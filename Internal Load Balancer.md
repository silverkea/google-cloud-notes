

- **Internal Application Load Balancer (L7)**
    
    - This is an **Envoy proxy-based, Layer 7** load balancer for internal **HTTP(S)** traffic.
        
    - It's a managed service that scales Envoy proxies for you.
        
    - It has two modes:
        
        - **Regional:** Clients and backends must be in the same region. This is useful for regional compliance.
            
        - **Cross-region:** Backends can be globally distributed. This provides high availability and automatic failover to the closest healthy backend.
            
- **Internal Passthrough Network Load Balancer (L4)**
    
    - This is a **regional, Layer 4** load balancer.
        
    - It is **not a proxy**. It's a software-defined, "pass-through" service (built on Andromeda) that sends traffic directly from the client to the backend.
        
    - Clients _must_ be in the same region as the load balancer.
        
    - It supports a wide variety of protocols, including **TCP, UDP, ICMP, GRE, ESP**, and more.
        
    - All traffic stays internal to your VPC network and region, which simplifies security and lowers latency.
        
- **Internal Proxy Network Load Balancer (L4)**
    
    - This is an **Envoy proxy-based, Layer 4** load balancer for **TCP** traffic.
        
    - It **is a proxy**: it terminates the client's TCP connection and opens a _new_ one to the backend.
        
    - Like the L7 internal load balancer, it has two modes:
        
        - **Regional:** Clients and backends are in the same region.
            
        - **Cross-region:** Backends can be globally distributed, providing high availability and failover.
            
- **Example Use Case (3-Tier Web App)**
    
    - You can use an **external** load balancer for your (Tier 1) web servers.
        
    - Those web servers can then talk to an **internal** load balancer for your (Tier 2) application servers.
        
    - The application servers then talk to the (Tier 3) database.
        
    - This approach keeps your application and database tiers from being exposed to the internet, improving security.