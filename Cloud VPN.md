
## Types
Google Cloud offers two types of Cloud VPN gateways: HA VPN and Classic VPN. All Cloud VPN gateways created before the introduction of HA VPN are considered Classic VPN gateways.

### Classic VPN
- Securely connects on-premises network to Google Cloud VPC network through IPsec VPN tunnels
- Traffic travelling between the networks is encrypted by one VPN gateway and decrypted by the other VPN gateway
- Useful for low-volume connections
- SLA of 99.9%
- Supports site-to-site VPN, static routing, dynamic routing, IKEv1 and IKEv2 ciphers

### HA VPN
- Provides higher reliability with **99.99% SLA** (compared to Classic VPN's 99.9%)
- 99.99% SLA requires **two or four tunnels** minimum to guarantee 
- Can configure HA VPN gateway with one active interface and one external IP address, this does not provide a 99.99% SLA
- Two external IP addresses automatically provisioned, one for each of its fixed number of two interfaces,
- **Requires BGP** (dynamic routing) while Classic VPN supports both static and dynamic routing
- Designed for **both high and low-volume connections**
- Supports only **IKEv2** ciphers (compared to Classic VPN's support for both IKEv1 and IKEv2)
- Offers **automatic failover** between tunnels
- Features a **regional, redundant architecture** with two interfaces
- Provides **higher throughput** capabilities
- **Recommended for production workloads** requiring high availability
- Still uses IPsec for encryption/decryption like Classic VPN

### Recommended Topologies
#### HA VPN Gateway to Peer VPN Gateway Topology

![[cloud-vpn-ha-vpn-to-peer-vpn-gateway-topology.png]]

- Typical peer gateway configurations
	- HA VPN gateway to two separate VPN devices, each with own IP address
	- HA VPN gateway to one peer VPN device that has two IP addresses
	- HA VPN gateway to one peer VPN that has one IP address
- Two peer-side gateways allows for fault tolerance and upgrades / scheduled maintenance, and provides 99.99% availability. The `REDUNDANCY_TYPE` has value `TWO_IPS_REDUNDANCY`


#### HA VPN Gateway to AWS Virtual Private Gateway

![[cloud-vpn-ha-vpn-to-aws-peer-gateway-topology.png]]

- Can use wither a transit gateway or a virtual private gateway
- Only transit gateway supports equal-cost multipath (ECMP) routing to equally distribute traffic.
- Three components to set up
	- HA VPN gateway in Google Cloud with two interfaces
	- Two AWS virtual private gateways connected to HA VPN gateway
	- External VPN gateway resource in Google Cloud to represent AWS virtual private gateway
- Supported configuration uses four tunnels
	- Two tunnels from one AWS virtual private gateway to one interface of HA VPN gateway
	- Two tunnels from the other AWS virtual private gateway to the other interface of HA VPN gateway 

#### Two HA VPN Gateways Connected to Each Other

![[cloud-vpn-between-google-cloud-networks-topology.png]]

- Use HA VPN gateways in two GCP networks to connect them.
- From perspective of each HA VPN, two tunnels are created
- Connect interface 0 to interface 0 of the other HA VPN gateway, and interface 1 to interface 1 of the other HA VPN gateway
- Provides 99.99% availability


## Dynamic Routes

- Configuration of dynamic routes requires use of Cloud Router
- Cloud Router uses Border Gateway Protocol (BGP) to manage routes, so routes can be updated and exchanged without changing tunnel configuration
- To set up BGP, an additional IP address is assigned to each end of VPN tunnel. These must be link-local IP addresses in the `169.245.0.0/16` range and are not part of IP address space of either network



