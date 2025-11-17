
## 1. Core Concepts & Architecture

- **Definition:** A fully managed, serverless platform for running stateless containers.
    
- **Fit Criteria:**
    
    - Stateless applications (local file system is ephemeral).
        
    - Listens on a configurable port (default 8080).
        
    - Handles HTTP, HTTP/2, WebSockets, or gRPC.
        
- **Two Operating Modes:**
    
    1. **Services:** Run continuously to handle web requests/events.
        
    2. **Jobs:** Perform work and quit (run to completion).
        
- **Execution Environments:**
    
    - **First Generation (Default for Services):** Fast cold start, system call emulation.
        
    - **Second Generation (Default for Jobs):** Full Linux compatibility, slower cold start, supports Network File Systems (NFS).
        

---

## 2. Container Lifecycle

The lifecycle manages how containers spin up and down to handle traffic and costs.

1. **Starting:** Cloud Run pulls the image (from internal storage) and starts the application. It probes port 8080 to check readiness.
    
2. **Serving Requests:** The container is active and handling traffic.
    
3. **Idle:** If no requests occur for **100ms**, the container becomes idle.
    
    - CPU is throttled to nearly zero (unless "CPU always allocated" is set).
        
    - No billing for idle time (unless "CPU always allocated" is set).
        
4. **Shutting Down:**
    
    - Triggered when scaling down.
        
    - Sends a **SIGTERM** signal to the application.
        
    - **Grace Period:** You have **10 seconds** to clean up (close DB connections, flush buffers) before the container is killed.
        
5. **Stopped:** The container disappears. Data in memory/ephemeral storage is lost.
    

> **ACE Exam Tip:** Always handle `SIGTERM` in your code to prevent data corruption during scaling events.

---

## 3. Deployment & Revisions

- **Source:** Images are pulled from **Artifact Registry** (recommended) or Docker Hub.
    
- **Revisions:**
    
    - Every deploy creates a new **Revision**.
        
    - Revisions are **immutable** (cannot be changed once created).
        
    - Any configuration change (env vars, memory, concurrency) creates a new revision.
        
- **Traffic Management:**
    
    - **Splitting:** You can split traffic between revisions (e.g., 90% to stable, 10% to new).
        
    - **Pinning:** You can send 100% traffic to a specific revision (rollback).
        
    - **Tagging:** Assign a custom URL (e.g., `green---app-url`) to a specific revision for testing without routing public traffic to it.
        

---

## 4. Autoscaling & Performance

Cloud Run scales automatically based on incoming request load.

### Scaling Boundaries

- **Scale to Zero:** Default behavior. If no requests, 0 instances run (Zero cost).
    
    - _Downside:_ **Cold Starts** (latency for the first request while container loads).
        
- **Min Instances:** Keeps a set number of "warm" instances idle to minimize cold starts. _Note: You pay for these idle instances_.
    
- **Max Instances:** Limits total instances to control costs or protect downstream databases (e.g., preventing connection pool exhaustion).
    

### Concurrency

- **Definition:** The maximum number of concurrent requests _one_ container instance can handle.
    
- **Default:** 80 requests per container.
    
- **Maximum:** Can be increased to 1,000.
    
- **When to lower:** If your app is not thread-safe or handles heavy CPU per request, set concurrency to 1.
    

---

## 5. Networking & Security

Ingress (Incoming Traffic)

1. **All:** Default. Public internet access allowed.
    
2. **Internal:** Only allows traffic from VPC, Internal Load Balancers, and other Google services (Pub/Sub, Eventarc) within the same project/perimeter.
    
3. **Internal and Cloud Load Balancing:** Allows internal traffic + traffic from Global External HTTP(S) Load Balancers (enables WAF/Cloud Armor protection).
    

### VPC Access (Outgoing Traffic)

To connect to private resources (Cloud SQL private IP, Memorystore, VM):

- Use a **Serverless VPC Access Connector**.
    
- Requires a `/28` subnet exclusively for the connector.
    
- Must be in the same region as the Cloud Run service.
    

### IAM & Service Identity

- **Invoker Role:** To make a service public, grant `roles/run.invoker` to `allUsers`. For private service-to-service, grant it to the calling service account.
    
- **Service Identity:**
    
    - **Default:** Uses the Compute Engine default service account (Project Editor role) -> **Security Risk**.
        
    - **Best Practice:** Create a **user-managed service account** with minimal permissions (Principle of Least Privilege).
        

---

## 6. Configuration & Secrets

- **Environment Variables:**
    
    - Injected at startup.
        
    - Changes require a new revision.
        
- **Secrets (Secret Manager):**
    
    - **Method 1: Environment Variable:** Value is determined at startup. Pinned to a specific version.
        
    - **Method 2: Volume Mount:** Mounted as a file. Can update dynamically to `latest` value without redeploying (though app must re-read file).
        
    - **Permission:** Service account needs `Secret Manager Secret Accessor` role.
        

---

## 7. Integrations

- **Pub/Sub:** Pushes messages to the Cloud Run endpoint via HTTP request. Service must acknowledge (200/204) or Pub/Sub retries.
    
- **Cloud SQL:**
    
    - **Public IP:** Connect via Cloud SQL Auth Proxy (Unix socket).
        
    - **Private IP:** Connect via Serverless VPC Connector.
        
- **Cloud Code:** IDE extension (VS Code/IntelliJ) for local development, debugging, and emulation before deploying.
    

---

## 8. CLI Cheat Sheet (gcloud)

- **Deploy from source:**
    
    `gcloud run deploy --source .`
    
- **Deploy image:**
    
    `gcloud run deploy --image gcr.io/project/image`
    
- **Make Public:**
    
    `gcloud run deploy --allow-unauthenticated`
    
- **Set Concurrency:**
    
    `gcloud run services update <service> --concurrency 80`
    
- **Set Min Instances:**
    
    `gcloud run services update <service> --min-instances 3`
    
- **Map Custom Domain:** Use Cloud Run Integrations.