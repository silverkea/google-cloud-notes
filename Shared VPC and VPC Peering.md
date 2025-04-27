
## Shared VPC
Allows organization to connect resources from multiple projects to a common VPC network so communication via internal IP address is possible

- One project designated as host, other projects attached as service projects
- Projects not participating are called standalone projects
- VPC networks in host project are called Shared VPC networks
- Resources from service projects can use subnets in Shared VPC network
- Allows organization admins to delegate responsibilities like creating and managing instances to Service Project Admins while maintaining central control over network resources like subnets, routes, firewalls

## VPC Peering
Allows private RFC 1918 connectivity across two VPC networks, regardless of whether they belong to same project or same organization

- Each organization has its own organization node, VPC network, VM instances, Network Admin, Instance Admin
- To establish VPC Network Peering, the admin of each network needs to peer their network with the other network.
- When both peering connections are created, VPC Network Perring sessions become Active and routes are exchanged, allowing instances to communicate via private IP address.
- Enables decentralized / distributed approach to multi-project networking because each VPC network may remain under control of separate administrator groups and maintain own global firewall and routing tables.
- This approach has better latency, security and cost savings compared to using external IPs or VPNs.