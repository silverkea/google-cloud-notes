
## Interacting with Google Cloud
### Cloud Console
 - web based GUI
 
### Cloud Shell and Google Cloud CLI
- Cloud Shell included in Cloud Console
	- temporary VM with 5GB persistent disk storage and `gcloud` CLI pre-installed
- CLI can be [installed locally](https://cloud.google.com/sdk/docs/install)

### REST-based API
- App APIs - provide access to services, with client libraries for supported languages
- Admin APIs - functionality for resource management, e.g. for building own automated tools

### Cloud Mobile App
- Manage cloud services from android / iOS device
- e.g. start, stop and ssh to [[Compute Engine]] instances and see logs


## Virtual Networks

### [[Virtual Private Cloud]]

#### Projects
- Encompass every service and resource in Google Cloud including networks
- Associates objects and services with billing
- Default quota is 15 networks, can be increased by request via Google Cloud console
#### Networks
- Provided in three modes:
	- **Default** 
		- Automatically created with every project
		- One subnet per region with non overlapping CIDR blocks
		- Default firewall rules allowing ingress traffic for ICMP, SSH and RDP from anywhere and ingress traffic from within default network for all protocols and ports
	- **Auto mode** 
		- Automatically creates one subnet in each region
		- Default network is actual an Auto mode network
		- Subnets use predefined IP ranges with /20 mask that can be expanded to /16
		- Subnets fit within the 10.128.0.0/9 CIDR block
		- As new regions are added, new subnets are created from that block
	- **Custom mode** - manually create subnets in regions
		 - Does not automatically create subnets in regions
		 - Allows complete control over subnets and IP ranges
		 - IP ranges cannot overlap between subnets of the same network
		 - Auto mode can be converted to Custom mode network, one way conversion
		 - IPv6 supported in custom mode networks
- Networks can be shared between projects or peered with networks in other projects
- Networks have no IP address ranges but are construct of all individual IP address and services within a network
- Google Cloud networks are global, spanning all available regions
- Can be segregated into regional subnetworks
- Virtual Machines in the same network can communicate using internal IP addresses even if they are in different regions
- VMs in different networks can communicate using external IP addresses only, even if in the same region. Traffic doesn't go via internet but via Google Edge routers.

[Learn More](https://www.cloudskillsboost.google/catalog?keywords=Networking+in+Google+Cloud&locale=)
#### Subnetworks
- Allows for network segmentation at regional scale and can cross zones within a region.
- Subnet is an IP address ranges within a network
- First and second addresses (.0 and .1) are reserved for the network and the subnet's gateway respectively
- VMs in different zones can communicate via same subnet IP address
- Single firewall rule can be applied even though VMs are in different zones
- IP address space of any subnet can be increased without any downtime, must follow rules
	- Subnets must not overlap other subnets in the VPC network
	- Each IP range for all subnets in VPC must be unique and valid CIDR block
	- Subnet IP address ranges are regional internal IP addresses and have to fall within valid IP ranges
	- Subnet ranges cannot match, be narrower or broader than a restricted range
	- Subnet ranges cannot span a valid RFC range, multiple RFC ranges or a privately used public IP address range
	- New subnet range must be larger than the existing range - can't undo expansion
	- Auto mode subnets start with /20 range and can be expanded to /16 but no larger, if larger range is required, auto mode can be converted to custom
- Avoid creating overly large subnets to avoid CIDR range collisions.

#### Regions & Zones


#### IP Addresses
- Each VM can have two IP addresses:
	- **Internal IP address** 
		- private IP address within a VPC network assigned via DHCP
		- symbolic names of VMs are registered with internal DNS scoped to network that translate to internal IP address
	- **External IP address** (optional) 
		- public IP address that can be accessed from the internet
		- can be static or ephemeral (assigned from a pool)
		- static IP addresses not assigned to a resource are charged at higher rate than static or ephemeral IP addresses assigned to a resource
		- can use own publicly routable IP addresses as Google Cloud external IP addresses, to be eligible must bring a /24 block or larger
		- external IP address is unknown to OS of VM, it is mapped to internal IP by the VPC
		- network stores a lookup table of external to internal IP address mappings

##### Alias IP Ranges
- Allows to assign multiple IP addresses to a single VM instance
- Useful if you have multiple services (e.g. multiple containers or applications) running on a single VM and want to assign different IP addresses to each service without having to define a separate network interface

##### IP Addresses for Default Domains 
Google publishes the complete list of IP ranges that it announces to the internet in goog.json. Google also publishes a list of Google Cloud customer-usable global and regional external IP addresses ranges in cloud.json. 

The following files replace the spf.google.com TXT records previously recommended to use for listing Google IP addresses. 
- https://www.gstatic.com/ipranges/cloud.json provides a JSON representation of Cloud IP addresses organized by region. 
- https://www.gstatic.com/ipranges/cloud_geofeed is a standard geofeed formatted IP geolocation file that we share with 3rd-party IP geo providers like Maxmind, Neustar, and IP2Location. 
- https://www.gstatic.com/ipranges/goog.json and https://www.gstatic.com/ipranges/goog.txt are JSON and TXT formatted files respectively that include Google public prefixes in CIDR notation. 
 
For more information as well as an example of how to use this information, refer to https://cloud.google.com/vpc/docs/configure-private-google-access#ip-addr-defaults

#### DNS
- Two types of DNS
	- Zonal
		- recommended because of higher reliability guarantees by isolating DNS failures in DNS registration to individual zones
	- Global (project wide)
- VM instances have hostname (same as instance name) that can be resolved to internal IP address
- There is also an internal fully qualified domain name (FQDN) that can be resolved to internal IP address
	- FQDN format is `{hostname}.{zone}.c.{project-id}.internal`
- IP address can change when instances are deleted and recreated
- Each instance has metadata server that acts as DNS for that instance
- Metadata server handles DNS queries for local network resources, and routes other queries to Google public DNS
- Public DNS records pointing to instance are not published automatically, admins can publish them using existing DNS servers.
- Google Cloud DNS is a managed DNS service that provides domain name resolution for applications running in Google Cloud using global network of Anycast name servers and offers 100% uptime SLA for domains configured in Cloud DNS

#### Routes
- Networks have default routes that allow instances to send traffic to each other, even across subnets
- Networks also have default route for sending packets to destinations outside the network
- These cover most needs, special routes can be created for specific needs
- Routes match packets by destination IP address
- Firewall rules must also allow packets to flow
- A route is created when a network is created, enabling traffic from 'anywhere'
- Routes are created automatically when a subnetwork is created enabling instances on same network to communicate
- Each route may apply to one or more instances
- A route applies to an instance if the network and instance tags match
- If a network matches and there are no tags, the route applies to all instances in the network
#### Firewall Rules
- Default networks have pre-configured firewall rules allowing all instances to communicate
- Manually created networks do not have pre-configured firewall rules
- GCP firewall rules protect instance from unapproved inbound (ingress) and outbound (egress) connections
- VPC functions as a distributed firewall - rules are applied to the network but connections are allowed or denied at instance level
- If all firewall rules are deleted, there is still a "Deny all" ingress rule and an "Allow all" egress rule for the network
- Rules are comprised of the following:
	- **Direction**
		- Ingress - incoming traffic
		- Egress - outgoing traffic
	- **Source or Destination** 
		- IP address or CIDR block of the source of the traffic
		- Can also be a tag or service account
	- **Protocol**
		- TCP, UDP, ICMP, ESP, AH or ALL
	- **Port**
		- Port number or range of ports
	- **Action**
		- Allow - allow traffic
		- Deny - deny traffic
	- **Priority**
		- Lower number means higher priority
		- Default is 1000
		- If two rules match, the one with the highest priority is applied
	- **Assignment**
		- Specifies which instances the rule applies to
		- Can be all instances  in the network (default) or a specific instance


#### Cloud NAT
- Managed network address translation service
- Allows instances without external IP addresses to be provisioned and to connect to the internet
- Best practice is to not provide external IP address wherever possible
- Cloud NAT does not implement inbound NAT, only outbound NAT

#### Private Google Access
- Allows instances without external IP addresses to connect to Google APIs and services
- e.g. if private VM instance needs to access a Cloud Storage bucket, Private Google Access needs to be enabled
- Private Google Access is enabled on a subnet-by-subnet basis