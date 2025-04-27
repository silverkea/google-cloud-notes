

## Cloud Interconnect

![[cloud-interconnect-option-comparison.png]]


### Dedicated Interconnect
- Physical connection between on-premises network and Google Cloud
- More cost effective than purchasing additional bandwidth over public internet
- Provision cross connect between Google network and own router in a colocation facility
- Configure BGP session over interconnect between Cloud Router and on-premises router to exchange routes between networks
- Can be configured for 99.9 or 99.99% uptime SLA

### Partner Interconnect
- Connectivity between on-premises network and VPC network via supported service provider
- Useful if data center is in physical location that cannot reach Dedicated Interconnect facility or if data needs don't warrant Dedicated Interconnect
- BGP session is established between your Cloud Router and on-premises router to start passing traffic between your networks via the service provider's network
- Can be configured to offer a 99.9% or a 99.99% uptime SLA between Google and the service provider

### Cross-Cloud Interconnect
- High-bandwidth dedicated connectivity between Google Cloud and another cloud provider
- Peer you Google VPC with network hosted by supported cloud service provider
- Supports AWS, Azure, Oracle Cloud Infrastructure, Alibaba Cloud
- Available in 10Gbps and 100 Gbps sizes
- Google does not guarantee uptime from other cloud provider, and cannot create support tickets on your behalf


## Cloud Peering

Allows establishment of direct peering connection between your network and Google's at one of Google's edge network locations

![[cloud-peering-options-comparison.png]]

### Direct Peering
- Exchange BGP routes between your network and Google's network
- Does not have an SLA
- Need to satisfy peering requirements
- GCP's Edge Points of Presence, or PoPs, are where Google's network connects to the rest of the Internet via peering
- 10 Gbps capacity per link

### Carrier Peering
- If you require access to Google public infrastructure and cannot satisfy Goggle's peering requirements, you can connect via a carrier peering partner
- Does not have an SLA
- Capacity depends on the service provider


## Choosing Connection Type


![[connection-options-dedicated-shared-layers.png]]


![[connection-options-interconnect-peering.png]]


![[connection-options-google-workspace.png]]

![[connection-options-other-cloud-provider.png]]

![[connection-options-on-premises.png]]


