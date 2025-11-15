
## Containers

- Isolated user spaces for running application code
- Lightweight because they don't carry full operating system
- Can be scheduled or integrated tightly with underlying system
- Created and shut down quickly because not booting entire VM or initializing OS

### Benefits to developers
- Code centric way to deliver high performing scalable applications
- Access to reliable underlying hardware and software
- Confidence code will run successfully regardless if on local machine or production
- Incremental changes made based on production image can be deployed with single file copy
- Easier to build microservices - loosely coupled fine grain components
- Can scale and upgrade components of application without affecting application as a whole 

### Isolation Workloads
Ability to isolate workloads comes from several Linux technologies
- Linux process - each has own virtual memory address space, can be rapidly created and destroyed
- Linux namespaces - used by containers to control what application can see - process id numbers, directory trees, IP addresses, etc
	- Note: different from Kubernetes namespaces
- Linux cgroups - control what an application can uses - CPU time, memory, I/O bandwidth, other resources
- Union file systems - allows bundling everything into neat package combining application and dependencies into set of clean minimal layers

### Container Image
- Structured in layers and built from file called container manifest - e.g. Dockerfile
- Instructions in manifest specify layers inside container image
- Each layer is read-only, but when container runs it will have writable ephemeral topmost layer

### Application Packaging
- Not best practice to build application in same container where you ship and run it
- Build tools are clutter and could increase attack surface
- Application packaging relies on multi-stage build process where one container builds final executable image, and separate container receives only what is needed to run application
- When launched from image, container runtime adds new ephemeral writable layer on top of underlying layers - called container layer
- Because it is ephemeral, permanent data must be stored elsewhere

### Container Registries
- Common to use publicly available open-source container images as base for your own images or unmodified use
- Google maintains [[Artifact Registry]] [pkg.dev](https://pkg.dev)
	- contains public open source images
	- storage for custom images private to projects that integrates with IAM 
- Others: Docker Hub, GitLab

### [[Cloud Build]]
- Managed service for building containers

## [[Kubernetes]]

Kubernetes is an open source container orchestration system for automating computer application deployment, scaling, and management.

Google developed Kubernetes (GKE) originally to support their own internal operations and then made it available as open source technology.


## GKE

Containers in GKE are based on images which are shared via [[Artifact Registry]]

GKE consists of multiple [[Compute Engine]] instance grouped together to form a cluster.

Can create Kubernetes clusters with Kubernetes Engine by using Google Cloud Console, gcloud command line tool from Cloud SDK, or REST API.

To start a Kubernetes cluster on GKE, run:

```
gcloud container clusters create k1
```

### Benefits

- Managed Kubernetes service hosted on Google's infrastructure
- Designed to deploy, manage, and scale Kubernetes environments for containerized applications
- Fully managed service with no need to provision underlying resources
- Uses container-optimized operating system for running workloads
- Google maintains and optimizes operating systems for quick scaling with minimal resource footprint


## GKE vs Open Source Kubernetes

### User Perspective

- Much simpler than managing open source Kubernetes
- GKE manages all control plane components
- Still exposes IP address for Kubernetes API requests
- GKE provisions and manages control plane infrastructure
- Eliminates need for separate control plane

## Node Management Modes

### Autopilot Mode (Recommended)

**Overview**: Optimized for production with hands-off Kubernetes management experience. Less management overhead but fewer configuration options.

**Key Benefits**:

- **Production Optimized**:
    
    - Google-managed and optimized GKE instance
    - Creates clusters using battle-tested, hardened best practices
    - Defines underlying machine types based on workloads
    - Optimizes usage and cost, adapts to changing workloads
    - Faster deployment of production-ready clusters
- **Strong Security Posture**:
    
    - Google secures cluster nodes and infrastructure
    - Eliminates infrastructure security management tasks
    - Locks down nodes to reduce attack surface
    - Prevents ongoing configuration mistakes
- **Operational Efficiency**:
    
    - Google monitors entire cluster (control plane, worker nodes, core Kubernetes components)
    - Ensures Pods are always scheduled
    - Keeps clusters always up to date
    - Configurable update windows for minimal workload disruption
    - Google fully responsible for optimizing resource consumption
- **Cost Optimization**: Pay only for Pods, not nodes (pay for what you use)


**Restrictions**:

- More restrictive configuration options than Standard mode
- Limited access to node objects
- No SSH or privilege escalation
- Limitations on node affinity and host access
- All Pods scheduled with Guaranteed Quality of Service (QoS) class

**Infrastructure Management**:

- Node configuration
- Autoscaling
- Auto-upgrades
- Baseline security configurations
- Baseline networking configuration

### Standard Mode

**Overview**: Provides fine-grained control with more configuration options but requires more management overhead.

**Key Characteristics**:

- Same functionality as Autopilot mode
- You are responsible for:
    - Configuring individual nodes
    - Managing the cluster
    - Optimizing the cluster
- More configuration flexibility
- Pay for all provisioned infrastructure regardless of usage

**Recommendation**: Not recommended unless specific level of configuration control is required.


## Key Features

- **Cluster creation**: GKE creates and sets up Kubernetes clusters
- **Auto-upgrade**: Ensures clusters are always upgraded with latest stable Kubernetes version
- **Node management**: Virtual machines that host containers are called nodes
- **Node auto-repair**: Performs periodic health checks and recreates unhealthy nodes
- **Cluster scaling**: Supports scaling the cluster itself, not just workloads

## Integrated Services

- **Cloud Build**: Uses private container images from Artifact Registry for automated deployment
- **IAM**: Controls access using accounts and role permissions
- **Google Cloud Observability**: Provides insights into application performance
- **Virtual Private Clouds**: Provides network infrastructure including load balancers and ingress access
- **Google Cloud Console**: Offers insights into clusters and resources with viewing, inspection, and deletion capabilities

## Dashboard Benefits

- More powerful dashboard compared to open source Kubernetes dashboard
- No need to manage dashboard setup and security
- Ready-to-use interface for GKE clusters and workloads

## Advanced Cluster Management Features

- Google Cloud's load balancing for [[Compute Engine]]
- Node pools for designating subsets of nodes in a cluster for additional flexibility
- Automatic scaling of cluster's node instances
- Automatic upgrades for clusters node software
- Node auto-repair to repair node health and availability
- Logging and monitoring with [[Google Cloud Observability]]



 
 
