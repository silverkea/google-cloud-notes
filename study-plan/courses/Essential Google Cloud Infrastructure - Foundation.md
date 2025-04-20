
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


## Virtual Machines

VMs consist of a virtual CPU, memory, disk and networking.

### [[Compute Engine]]

- Infrastructure as a Service (IaaS) offering
- Predefined or custom machine types
	- vCPUs (cores) and Memory (RAM)
	- Storage
		- Zonal or regional persistent disks
		- Local SSD
		- Cloud Storage
	- Networking
	- Linux or Windows

#### TPUs (Tensor Processing Units)
- Custom hardware accelerator for machine learning workloads developed by Google
- Domain-specific hardware, as opposed to general purpose hardware with CPUs and GPUs
- Allow for higher efficiency by tailoring architecture to meet computation needs in a domain such as matrix multiplication in machine learning.
- Faster and more energy efficient than GPUs and CPUs for AI applications and machine learning.
- Recommended for models that train for long durations.

#### CPU
- Each CPU (or vCPU) is implemented as a single hardware hyper-thread on one of the available CPU platforms
##### Network Throughput
- Network will scale at 2 gigabits per second for each CPU core
- Instances with 2 or 4 CPUs receive up to 10 gigabits per second
- Theoretical maximum of 200 gigabits per second for 176 vCPU on C3 machine series

#### Disk
- Options
	- Standard - spinning hard disk drives - higher capacity per dollar - up to 257 TB per instance
	- SSD - solid state drives - higher IOPS per dollar - up to 257 TB per instance
	- Local SSD 
		- physically attached to the host machine, faster than persistent disks but not replicated
		- higher throughput at lower latency
		- stored data only persisted until VM stopped or deleted
		- typically used as a swap disk or for temporary data

#### Networking
- Auto, custom networks
- Inbound / outbound firewall rules
	- IP based
	- Instance / group tags
- Application Load Balancing
- Network Load Balancing
	- Does not require pre-warming
	- Set of traffic engineering rules applied to IP address subnet range
- Global and multi-regional subnets


#### VM Access and Lifecycle

##### Linux: SSH
- SSH from Cloud Console or Cloud Shell via Cloud SDK
- SSH from computer or third-party client and generated key pair
- Requires firewall to allow `tcp:22` ingress traffic

##### Windows: RDP
- RDP clients
- Powershell terminal
- Requires setting Windows password
- Requires firewall rule to allow `tcp:3389` ingress traffic

##### VM Lifecycle

![[vm-lifecycle.png]]


###### Provisioning
- CPU, memory, disks being reserved, instance not running yet
###### Staging
- Resources have been acquired and instance is prepared for launch
- Adding IP addresses, booting system image, booting OS
###### Running
- First executes startup scripts and enable SSH or RDP access
- Running instance can be live migrated to another host machine in same zone
	- Allows maintenance by Google without downtime
- Can also move instance to another zone, take snapshot of persistent disk, export system image or reconfigure metadata
- Some actions require stopping, such as adding CPU and memory
- Also have option to reset instance. Stays in Running state throughout, wipes memory and resets the VM to initial state
- Can perform these actions
	- Add or remove attached non-boot disks, change auto-delete settings of non-boot disks
	- Modify instance tags
	- Modify custom CM or project-wide metadata
	- Remove or set a new ephemeral external IP and promote to static external IP address
	- Modify VM availability policy

###### Repairing
- Occurs when VM encounters error or underlying host unavailable due to maintenance
- VM unusable during this time, billing is paused
- SLA not applicable during this time

###### Stopping
- Run shutdown scripts before transitioning to Terminated state

###### Terminated
- Options to restart or delete
- While terminated there is no charge for memory or CPU, still charged for disks and reserved IP addresses
- Can perform these actions
	- Change machine type
	- Migrate VM to another network
	- Add or remove attached disks, change auto-delete settings
	- Modify instance tags
	- Modify custom CM or project-wide metadata
	- Remove or set a new static IP
	- Modify VM availability policy
- Image of a stopped VM can't be changed

###### Suspending
- Transitory state before being suspended. 

###### Suspended
- Options to resume or delete

While rebooting, stopping or deleting an instance, shutdown will take about 90 seconds.

For a preemptible VM, if the instance does not stop after 30 seconds, Compute Engine sends an ACPI G3 Mechanical Off signal to the operating system.

If VM is terminated by crash or maintenance event, default behaviour is to restart. Behaviour can be changed in availability policies by configuring `Automatic restart `and `On host maintenance` options. Can be changed while machine is running.


##### OS Patch Management
- Apply operating system patches across a set of compute engine VM instances
- Patch compliance reporting 
	- insights into patch compliance across VM instances
	- recommendations for VM instances
- Patch deployment
	- automates OS and software patch update process
	- schedules patch jobs
	- patch job runs across VM instances and applies patches
- Capabilities
	- Create patch approvals
	- Select patches to apply
	- Set up flexible scheduling - choose when to apply patches - one time and recurring schedule
	- Apply advanced patch configuration settings
		- Pre and post patching scripts
	- Manage patch jobs or updates from central location

#### Machine Creation Options

VMs can be created via Google Cloud console, Cloud Shell, Google Cloud CLI, REST API or Terraform.

When creating a VM, a machine type is selected from a machine family and machine series. Predefined or custom machine type can be chosen from machine family.


##### General Purpose Machine Family
Best price-performance with most flexible vCPU to memory ratio. Suitable for most workloads.

###### E2 Series
- Day to day workloads, web servers, small databases, development and test environments, applications that don't have strict performance requirements. 
- Contain shared-core machine types that use context switching to share physical cores between vCPUs for multitasking.
- Cost effective for small non resource intensive applications than standard, high memory or high CPU machine types
- Comparable baseline performance with N1 series VMs
- 2 - 32 CPUs, 0.5GB to 8GM of memory per CPU

###### N2 and N2D Series
- Most flexible VMs, balance between prices and performance
- Wide range of VM shapes, including enterprise applications, medium-to-large databases, and many web and app-serving workloads.
- N2 - up to 128 vCPUs and 0.5GB to 8GB of memory per vCPU
- N2D - AMD EPYC processors, up to 224 vCPUs and 0.5GB to 8GB of memory per vCPU

###### Tau T2A and T2D Series
- Cost effective performance for scale-out workloads - web servers, containerized microservices, media transcoding, large scale applications
- Supported by [[Google Kubernetes Engine|GKE]] to help optimize price performance. 
- T2A - Arm-based processors, up to 64 vCPUs and 0.5GB to 8GB of memory per vCPU
- T2D - AMD EPYC processors, up to 60 vCPUs and 4GB of memory per vCPU

##### Compute-optimized Machine Family
Highest performance per core, optimized for compute intensive workloads

###### C2 Series
- AAA gaming, electronic design automation, high performance computing across simulations, genomic analysis, media transcoding
- Applications that have expensive per core licensing, thus benefiting from higher performance per core
- 4 - 60 vCPUs, up to 240 GB memory

###### C2D Series
- Largest VM sizes, best suited for high performance computing
- 4 - 224 vCPUs, up to 896 GB memory, up to 3 TB local storage

###### H3 Series
- Offer 88 vCPUs and 352 GB of memory

##### Memory-optimized Machine Family
- Provide most compute and memory resources of any machine family
- Ideal for workloads requiring high memory to vCPU workloads
- Large in memory databases, in memory analytics workloads, genomic modeling, electronic design automation, high performance computing
- Lowest cost per GB of memory
- Up to 30% sustained use discounts, and up to 60% committed use discounts for 3 year commitment

###### M1 Series
- Up to 4TB of memory

###### M2 Series
- Up to 12 TB of memory

##### Accelerator-optimized Machine Family
- Ideal for massively parallelized Compute Unified Device Architecture workloads like machine learning and high performance computing
- Optimal choice for workloads that require GPUs
- Suited for CUDA-enabled ML training and inference, video transcribing, remote visualization workstations

###### A2 Series
- 12 - 96 vCPUs, up to 1360 GB of memory, up to 16 NVIDIA Ampere A100 GPUs

###### G2 Series
- 4 - 96 vCPUs, up to 432 GB of memory, up to 8 NVIDIA Ampere A100 GPUs

##### Custom Machine Types
- Allows to create a VM with custom CPU and memory configuration
- Suitable when workload doesn't fit any predefined machine types
- Workload requires more memory or processing, but don't need all the upgrades of next larger predefined machine type
- Costs are slightly higher for custom machine types
- 1 vCPU or and even number of vCPUs, 1GB - 8GB memory per vCPU standard (more available at extra cost as extended memory)


#### Compute Pricing

- Per second billing with minimum of 1 minute
	- vCPUs, GPUs and GB of memory
- Resource based pricing
	- Each vCPU, GB of memory billed separately
- Discounts
	- Sustained use
		- Automatic discounts applied when running for more than 25% of a month
		- Discount increases with usage, up to 30% net discount for running 100% of the month
		- For full benefit, create instances on first day of the month
	- Committed use - 1 or 3 years
		- Up to 57% for most machine types or custom machine types
		- Up to 70% for memory optimized machine types
	- Preemptible and Spot VM instances
		- Excess Compute Engine capacity at lower prices, availability varies with usage
		- Preemptible VMs can only run for up to 24 hours
		- Spot VMs don't have a maximum runtime
- Recommendation Engine
	- Notifies of underutilized instances
- Free usage limits


#### Preemptible VMs
- Lower price for interruptible workloads - up to 91% discount
- Might be terminated at any time
	- No charge if terminated in first minute
	- 24 hours max
	- 30 second termination warning, not guaranteed
- No live migrations or automatic restarts
- Can create monitoring and load balancers to start new preemptible VMs in case of failure
- Suitable for batch processing where if some instances terminate the job slows but doesn't stop
	- Complete batch jobs without placing load on existing instances, and at lower cost

#### Spot VMs
- Latest version of preemptible VMs
- Same pricing model as preemptible VMs
- No maximum run time
- Capacity for Spot VMs often easier to get for smaller machine types - less vCPU and memory

#### Sole Tenant Nodes
- Physical Compute Engine server dedicated to hosting VM instances only for specific project
- Useful for workloads that require physical isolation from other customers
- Suitable for workloads that need to be isolated to meet compliance requirements such as payment processing
- Can fill node with multiple VM instances of varying sizes including custom machine types and instances with extended memory
- Existing operating system licenses can be used on sole-tenant nodes while minimizing physical core usage

#### Shielded VMs
- Verifiable integrity of VM instances 
- Prevent compromise by boot or kernel-level malware or rootkits
- Achieved through use of Secure Boot, virtual trusted platform module or vTPM-enabled Measured Boot and integrity monitoring
- First offering in Shielded Cloud Initiative, providing even more secure foundation for all of Google with features like vTPM shielding or sealing that help prevent data exfiltration
- Requires a shielded image

#### Confidential VMs
- Allows encryption of code and data during processing
- Easy to use, no change required to applications, doesn't compromise performance
- N2D Compute Engine VM running on second generation AMD EPYC processors
- Provides high memory capacity, high throughput, supports parallel and compute heavy workloads 
- Google does not have access to encryption keys

#### Images
- Includes boot loader, OS, file system structure, pre-configured software, other customizations
- Stores all configuration, metadata, permissions and data from one or more disks required to create VM instance
- Used for creation, backup and recovery, and instance cloning
- Can select public or custom image
- Some are premium images, indicated with a `p` in the image name
	- Will have per second charge after 1 minute minimum
	- SQL Server charged after 10 minute minimum
	- Prices vary by machine type, but are global and do not vary by region or zone
- Custom images can be created by pre-installing software authorized for organization
- Can import images from own premises or workstation, or another cloud provider
- Can share custom images with other projects and anyone in your project


#### Disk Options

##### Boot Disk
- VMs come with a single bootable disk, with image loaded to root on first boot
	- Bootable - attach to VM and boot from it
	- Durable - survives VM termination
- Some OS images are customizable for Compute Engine
- Can survive VM deletion if delete boot disk on deletion option is disabled

##### Persistent Disk
- Attached to VM through network interface
- Durable storage, can survive VM terminate
- Bootable
- Allows snapshots
- Scales with size
- HDD or SSD options
- Allows resizing even while running and attached
- Can be attached in read-only mode to multiple VMs
	- Allows sharing data between VMs, cheaper than replication
- Zonal or Regional
	- Zonal provides efficient reliable block storage
	- Regional provides active-active disk replication across two zones in same region
		- Good option for high-performance databases and enterprise applications requiring high availability
	- Can select from:
		- `pd-standard` - Standard - HDD - suitable for large data processing workloads and sequential I/Os
		- `pd-ssd` - Performance - SSD - suitable for high performance low latency workloads and more IOPS than standard provides
		- `pd-balanced` - Balanced - also backed by SSD and balance performance and cost. Same IOPS as SSD persistent and lower IOPS per gigabyte, suitable for most VM shapes
		- `pd-extreme` (zonal only) - Extreme - SSD - zonal persistent disk designed for high end database workloads requiring high performance for random I/O operations and bulk throughput. Can provision desired IOPS, unlike other disk types
- Data encrypted at rest automatically with Google-managed encryption keys
	- Can use Cloud Key Management Service to manage encryption keys (customer managed encryption keys) or create and manage own key encryption keys (customer supplied encryption keys)

##### Local SSD
- Physically attached to the VM host machine
- Ephemeral but provide very high IOPS
- Local SSDs are 375GB, can attach up to 24 local SSDs partitions, up to 9 TB total per instance
- Data will survive a reset but not a VM stop or terminate, cannot be reattached to different VM

##### RAM Disk
- `tmpfs` - store data in memory
- Faster than local disk, slower than memory
	- Use when app expects files system structure and cannot directly use memory
	- Fast scratch disk, or fast cache
- Volatile, erased on stop or restart
- May need larger machine type if RAM was sized for application
- Consider backup to persistent disk

##### Max Persistent Disks
- Shared core - max of 16
- Other machine types - max of 128
	- Standard, High memory, High-CPU, Memory optimized, Compute optimized

###### Throughput Limitations
- Throughput limited by the number of cores
- Throughput shares same bandwidth with Disk I/O
	- Large amount of Disk I/O will compete with network egress or ingress throughput
- Important consideration when a large number of disks are attached

##### Persistent Disk Management Differences

###### Computer Hardware Disk
- Partitioning, 
- Repartitioning, 
- Reformat, 
- Redundant disk arrays, 
- Sub-volume management and snapshots
- Encrypt files before write to disk

###### Cloud Persistent Disk
- Virtual networked device
- Single file system is best
- Resize (grow) disks
- Resize file system
- Build-in snapshot and redundancy services
- Automatically encrypted, can even use own keys


#### Common Compute Engine Actions

##### Metadata and Scripts
- VM instances store metadata on a metadata server
- Useful in combination with startup and shutdown scripts
- Can use metadata server to programmatically get unique info (key/value pairs) about an instance without additional authorization
- Keys are same on every instance, so can reuse script on all instances
- Recommend storing scripts in [[Cloud Storage]] bucket

##### Move Instance to New Zone or Region
- Requires shut down, move, then restart
- References to original VM need to be updated
- Some server generated properties of VM and disks will change
- High level process: Create image of source VM, create new VM in target zone, delete source VM

##### Snapshots - for persistent disks only, not available for local disks
- Example uses:
	- Back up critical data - store in [[Cloud Storage]]
	- Move data between zones or regions
	- Transfer data to a different disk type
- Different from public images and custom images
- Snapshots are incremental and automatically compressed, only changed blocks are copied
- Schedulable

##### Resize Persistent Disk
- Can be resized while VM is running
- Added benefit of increasing capacity is to improve I/O performance
- Can only grow disks, can never shrink them

