
- Acts at Layer 7 of the OSI model - Application layer
- Distribute HTTP / HTTPS to backends
- Deployment modes: External and Internal

## External Load Balancers
- Implemented using [[Google Front Ends]] (GFEs) or managed proxies
- Global external Application Load Balancers and classic Application Load Balancers use GFEs that are distributed globally, operating together by using Google's global network and control plane
- Global and regional ALB use open source Envoy proxy software for advanced traffic management capabilities

| **Feature**          | **Global External ALB (Modern)**                       | **Regional External ALB (Modern)** | **Classic ALB (Legacy)**                                        |
| -------------------- | ------------------------------------------------------ | ---------------------------------- | --------------------------------------------------------------- |
| **Underlying Tech**  | **Envoy Proxy**                                        | **Envoy Proxy**                    | Google Front End (GFE)                                          |
| **Scope**            | **Global** (Single anycast IP)                         | **Regional** (Single region)       | **Global** (if Premium Tier) or **Regional** (if Standard Tier) |
| **Network Tier**     | Premium Tier only                                      | Premium or Standard Tier           | Premium or Standard Tier                                        |
| **Advanced Traffic** | **Yes** (Traffic splitting, mirroring, rewrites, etc.) | **Yes** (Within its region)        | **No**                                                          |
| **Google's Advice**  | **Recommended for global apps**                        | **Recommended for regional apps**  | **Legacy** (Migrate to modern)                                  |


## Application Load Balancer architecture:

- Clients connect to a public **IP address and port**, which are defined by an **external forwarding rule**.
- This rule sends the request to a **target HTTP(S) proxy**.
- The proxy uses a **URL map** to make routing decisions based on the request's content. It also handles **SSL certificates** for HTTPS.
- The proxy forwards the request to a **backend service**, which groups one or more backends (e.g., instance groups or storage buckets).
- The backend service uses **health checks** to poll instances, ensuring traffic is only sent to healthy backends.
- Backend services also manage other settings like **session affinity** and **timeout** configurations.

### Request Distribution
- Backend services uses round-robin algorithm by default
- Can be overridden with session affinity to send requests from same client to same VM

### Timeout
- Backend service has timeout - how long to wait on backend before considering request timed out
- Default to 30 seconds as a fixed timeout not idle timeout
- Set this appropriately for long lived connections

### Backends
- Contain instance group, balancing mode and capacity scaler
- Instance group contains VM instances
- Instance group can be MIG with or without autoscaling, or unmanaged instance group
- Balancing mode tells load balancer how to determine when backend is at full usage
- If all backends for backend service in a region are at full usage, new requests automatically rout to nearest region with capacity
- Balancing mode can be CPU utilization or requests per second (RPS)
- Capacity is additional setting that interacts with balancing mode
	- e.g. For normal operation of 80% CPU set balancing mode to 80% CPU and capacity to 100%, to cut utilization in half, keep balancing mode at 80% and set capacity to 50%

### HTTPS
- Uses a target HTTPS proxy instead of target HTTP proxy
- Requires at least one signed SSL certificate installed on target HTTPS proxy - can be up to 15
- For each SSL certificate, you first create an SSL certificate resource, which contains the SSL certificate information
- Client SSL sessions terminate at the load balancer
- ALB supports the QUIC transport layer protocol
	- faster client connection initiation
	- eliminate head-of-line blocking in multiplexed streams
	- supports connection migration when client IP address changes

### Backend Buckets
- Allow use of [[Cloud Storage]] buckets with ALB
- ALB uses URL map to direct traffic to backend service or backend bucket

### Network Endpoint Group (NEG)
- Configuration object that specifies a group of backend endpoints or services
- Common use case is deploying services in containers
- Can also distribute traffic in granular fashion to applications running on backend instances
- Zonal and internet NEGs define how endpoints should be reached, whether they are reachable, and where they are located
- Serverless NEGs don't contain endpoints
- Zonal NEG contains one or more endpoints like VMs or services running on VMs, specified by IP address or `IP:port` combination
- Internet NEG contains a single endpoint hosted outside of Google Cloud, specified by `FQDN:port` or `IP:port`
- Serverless NEG points to [[Cloud Run]], [[App Engine]], [[Cloud Run Functions]] residing in same region as NEG




