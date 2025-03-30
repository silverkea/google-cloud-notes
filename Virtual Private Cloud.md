Google’s software defined networking stack is based on the idea of a Virtual Private Cloud. 

Provides a secure, individual, private cloud computing model hosted within Google’s public cloud infrastructure.

Combines scalability and flexibility of cloud computing with the security and control of a private network.

VPCs connect Google Cloud resources to each other and to the internet.

## Subnets

VPCs are global resources, but subnets are regional resources. 

Subnets are segmented parts of the larger network.

VPCs group regional resources into internal IP address ranges called subnets.

Resources can be in different zones on the same subnet. This means resources to be neighbours on the same subnet even if they are in different zones, allowing for solutions that are resilient to disruption yet retain a simple network layout.

Subnet size can be increased by expanding the range of IP addresses allocated to it.


## Routing Tables

Like physical networks, VPCs have routing tables.

Routing tables are built in, so you don't need to configure or provision a router.

Used to forward traffic from one instance to another in the same network, across subnetworks or between zones without requiring external IP address.

## Firewalls

VPCs provide global distributed firewall that allows control of incoming and outgoing traffic.

Firewall rules are defined through network tags on [[Compute Engine]] instances.

For example, servers can be tagged with `WEB` and rule configured to allow traffic on ports 80 and 443 to instances with the `WEB` tag regardless of their IP address.

## VPC Peering

Allows VPCs from different projects to be connected to exchange traffic with each other.

## Shared VPC

Allows connecting resources from multiple projects to a common VPC network to facilitate communication using internal IP addresses from that network.

One project is designated as the host project and the others as the service projects.

[[Identity and Access Management (IAM)]] can be used to manage and delegate administration of shared VPC resources.


## Cloud Load Balancing

Fully distributed, software defined, managed service that distributes user requests across multiple instances.

Load balancers don't run in VMs, so they don't have to worry about scaling or managing them.

Can put load balancing in front of all traffic - HTTP, HTTPS, TCP and SSL, and UDP.

Provides cross-region load balancing, including multi-region failover.

Responds quickly to changes in users, traffic, network, backend health and other conditions.


### Application Load Balancers

Operate at application layer, designed for HTTP and HTTPS traffic. 

Ideal for web applications that require features like SSL/TLS termination and content based routing.

Operate as reverse proxies, distributing traffic based on defined rules.

Can be configured for internet facing and internal applications.

### Network Load Balancers

Operate at the transport layer and efficiently handle TCP, UDP and other IP protocols.


#### Proxy Network Load Balancers

Function as reverse proxies, terminating client connections and establishing new ones to backend services.

Support backends located both on-premises and in various cloud environments.


#### Passthrough Network Load Balancers

Connections are not modified or terminated, but directly forwarded to the backend while preserving the client source IP.

Suited for applications thar require direct server return or need to handle a wider range of IP protocols.


## Cloud DNS

Managed DNS service running on the same infrastructure as Google.

Low latency, high availability with DNS information served from redundant locations globally.

Cloud DNS is also programmable.

Can be managed using Google Cloud console, CLI or API.


## Cloud CDN

Leverages Google's system of edge caches to store content closer to users.

- Reduces latency
- Reduce load on origin servers
- Lower serving costs

Can be enabled with a single checkbox in the Google Cloud console.

### CDN Interconnect

Enables select third-party providers to establish direct peering links with Google's edge network, enabling traffic to be directed from your VPC network to a provider's network.

#### CDN Interconnect Partners
- Akamai
- Cloudflare
- Fastly


## Connecting Networks to Google VPC

### Cloud VPN

- Virtual Private Network connection over internet to create a "tunnel" connection.
- Cloud Router used to make connection dynamic
- Cloud Router lets other networks and Google VPC exchange route information over the VPN using Border Gateway Protocol
- When new subnet added to Google VPC, on-premises network automatically gets routes to it.

### Direct Peering

- Locate a router in same public data center as Google point of presence to exchange traffic between networks
- Google has over 100 points of presence globally

### Carrier Peering

- Connect to Google network through a carrier partner
- Provides direct access from on-premises through a service provider's network to Google Cloud resources
- Not covered by Google's SLA

### Dedicated Interconnect

- One or more direct, private connections to Google
- Highest uptimes for interconnection
- If topologies meet Google's specification, they can be covered by SLA of 99.99% uptime
- Can be backed by a VPN for greater reliability

### Partner Interconnect

- Can be configured to support mission-critical workloads that can tolerate some downtime
- If topologies meet Google's specification, they can be covered by SLA of 99.99% uptime
- Google not responsible for aspects of the connection that are managed by the service provider

### Cross-Cloud Interconnect

- Google provisions a dedicated physical connection between Google network and another cloud provider
- Supports adoption of integrated multi-cloud strategy
- Supports various cloud providers
- Cloud Interconnect offers reduced complexity, site-to-site data transfer, encryption
- Available in two sizes - 10Gbps and 100 Gbps





