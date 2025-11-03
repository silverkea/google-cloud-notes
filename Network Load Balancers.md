- Network Load Balancers are **Layer 4** balancers that handle **TCP, UDP, and other IP protocols**.
- They come in two main types: **Proxy** (a reverse proxy) or **Passthrough** (not a proxy).
---
### Proxy Network Load Balancers

- These are reverse proxies (built on Google Front Ends or Envoy) that **terminate the client's connection** and then open a _new_ connection to the closest available backend.
- They are intended for **TCP traffic only**, with or without SSL. For HTTP(S) traffic, an Application Load Balancer is recommended.
- They can be deployed in **global, regional, or classic** modes to handle traffic from the internet.

---
### Passthrough Network Load Balancers

- These are **not proxies**; they pass traffic directly to the backend VMs.
- They **preserve the client's original source IP address**.
- They use **Direct Server Return (DSR)**, where the backend VM sends the response directly to the client, not back through the load balancer.
- Because they are passthrough, they support a wide variety of protocols, including **TCP, UDP, ESP, GRE, and ICMP**.
- Backends for passthrough LBs are configured using either:
    - **Backend Services (Recommended):** The modern, flexible option that supports IPv6, multiple backend types (MIGs, NEGs), and advanced health checks.
    - **Target Pools (Legacy):** The older method, limited to TCP/UDP traffic, which uses a hash to distribute traffic.

