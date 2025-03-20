

## Cloud Compute Options

### Virtual Machines

Multiple systems run on the same hardware.

Enabled by Hypervisor - software layer that runs on physical hardware and multiple VMs are built on top of it.

VMs recreate or virtualize a full representation of the hardware.
### Containerization

Same principle as virtual machines. Isolated environment to run software services and optimize resources from one piece of hardware, but more efficiently than VMs.

Containers only recreate or virtualize the operating system - only what is needed to run the application they support.

Start faster and use a fraction of memory compared to booting an entire virtual machine.

Can run virtually anywhere
- Linux, Windows, Mac
- Virtual machines
- Bare metal - directly on hardware
- Developer's machine
- In data centers / on premises
- Public cloud

#### Kubernetes
Open source cluster management system that provides automated container orchestration.

Simplifies the management of machines and services for you.

- Improves application reliability
- Reduces time needed for development and operations


### Google Virtualization Solutions

#### [[Compute Engine]]
Scalable high performance virtual machines.
- Boot quickly
- Persistent disk storage
- Consistent performance

#### [[Google Cloud VMware Engine]]
Fully managed service that lets you run VMware platform in the cloud

#### [[Bare Metal]]
Enables you to migrate specialized workloads to the cloud while maintaining existing investments and architecture

#### [[Google Kubernetes Engine]] (GKE)
Managed environment for deploying, managing and scaling your containerized applications on Google infrastructure


### Serverless Computing

Resource such as compute power are automatically provisioned behind the scenes automatically.

Businesses provide the code for what they want and the cloud provider handles the rest.

Also known as Function as a Service

### Google Serverless Solutions

#### [[App Engine]]
PaaS platform for developing and hosting web applications.
Allows developers to build scalable web and mobile backends in any language on fully managed serverless platform.

#### [[Cloud Run]]
Allows developers to build applications in favorite programming languages and deploy them in seconds.
Scale up and down from zero almost instantly depending on user traffic.

#### [[Cloud Run Functions]]
Serverless execution environment for building and connecting cloud services.
Scalable, pay as you go functions as a service to run you code with zero management.
Simple and intuitive developer experience.
Write small code snippets that respond to events.


## [[Private Cloud]],  [[Hybrid Cloud]] and [[Multi Cloud]]

- [[Private Cloud]] - organization has virtualized servers in its own data centers to create private on-premises environment
- [[Hybrid Cloud]] - some combination of on-premises private cloud infrastructure and public cloud
- [[Multi Cloud]] - organization uses multiple public cloud providers to take advantage of key strengths of each provider


## [[Anthos]]

Open application modernization platform that enables you to modernize existing applications, build new applications and run them anywhere - on premises, Google cloud, or different public cloud.


## Secure Network

Google Cloud customers are able to run their applications and services on the same infrastructure that Google uses to serve billions of users around the world.

The network is truly global, operating in over 200 countries and territories with 20 regions and over 130 points of access.

This means that customers benefit from a private, well-provisioned, highly reliable global network.

## Sustainability

Net emissions of compute and storage in Google Cloud will be zero because Google matches 100% of energy consumed with renewable energy and maintains commitment to carbon neutrality.


