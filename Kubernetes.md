
- Open source platform for managing containerized workloads and services 
- Orchestrates many containers across multiple hosts 
- Enables scaling as microservices with easy deployment rollouts and rollbacks 
- Set of APIs for deploying containers on a cluster of nodes

## Architecture

- **Control plane**: Primary components that manage the system 
- **Nodes**: Computing instances (machines) that run containers 
- **Cluster**: Collection of nodes working together

## Configuration Approaches

- **Declarative configuration** (preferred):
	- Describe desired state rather than issuing commands
	- Kubernetes maintains this state automatically
	- Reduces errors and documents system state 

- **Imperative configuration**:
	- Issue direct commands to change system state
	- Used for quick fixes and building declarative configs

## Key Features

- **Workload support**:

	- Stateless applications (Nginx, Apache)
	- Stateful applications (persistent user/session data)
	- Batch jobs and daemon tasks

- **Auto-scaling**: Scales applications based on resource utilization

-  **Resource management**:

	- Users can specify resource requests and limits
	- Improves overall cluster performance

- **Extensibility**: Rich ecosystem of plugins and addons

	- Custom Resource Definitions for new resource types

- **Portability**:

	- Open-source and vendor-agnostic
	- Can deploy on-premises or any cloud provider
	- No vendor lock-in for workloads


## How Kubernetes Works

### Two Key Concepts

#### Kubernetes Object Model

- Each item Kubernetes manages is represented by an object
- You can view and change object attributes and state

#### Declarative Management Principle

- Tell Kubernetes how objects should be managed
- Kubernetes works to achieve and maintain desired state
- Accomplished through a "watch loop"

### Kubernetes Objects

#### Definition

- Persistent entity representing state of something running in a cluster
- Contains both desired state and current state
- Represents containerized applications, available resources, and behavior policies

#### Two Important Elements

- **Object spec**: Desired state defined by you when creating object
- **Object status**: Current state provided by Kubernetes control plane

#### Control Plane

- Term referring to various system processes that collaborate to make Kubernetes cluster work

### Pods

#### Basic Information

- Foundational building block of standard Kubernetes model
- Smallest deployable Kubernetes object
- Every running container in Kubernetes system is in a Pod

#### Pod Environment

- Creates environment where containers live
- Can accommodate one or more containers
- Multiple containers in Pod are tightly coupled and share resources

#### Networking and Storage

- Each Pod gets unique IP address
- All containers within Pod share network namespace (IP address and network ports)
- Containers in same Pod communicate through localhost (127.0.0.1)
- Pod can specify storage volumes shared among containers

### Example: Three Nginx Web Servers

#### Scenario

- Want three nginx Web server instances
- Each in own container
- Always kept running

#### Implementation Process

- Declare objects to represent nginx containers (Pods)
- Kubernetes launches and maintains those Pods
- Desired state: three nginx Pods always running

#### State Management

- Kubernetes compares desired state to current state
- If current state doesn't match desired state, control plane remedies situation
- If 0 Pods running but 3 desired, Kubernetes launches 3 Pods
- Control plane continuously monitors cluster state
- Endlessly compares reality to declared state and remedies as needed


## Kubernetes Control Plane Overview

The Kubernetes control plane is the fleet of cooperating processes that make a Kubernetes cluster work. Understanding these components helps illustrate how GKE clusters are easier to manage than self-provisioned ones.

## Cluster Architecture

- **Computers needed**: Usually virtual machines (always VMs in GKE, could be physical)
- **Control plane**: One computer that coordinates the entire cluster
- **Nodes**: Other computers whose job is to run Pods

## Control Plane Components

### kube-APIserver

- Only component you interact with directly
- Accepts commands that view or change cluster state (including launching Pods)
- Authenticates incoming requests and determines authorization/validity
- Manages admission control
- All cluster state queries or changes must go through kube-APIserver

### kubectl

- Command that connects to kube-APIserver
- Communicates using the Kubernetes API

### etcd

- Cluster's database
- Reliably stores cluster state including:
    - All cluster configuration data
    - Dynamic information (nodes, Pods, Pod placement)
- Never interact with etcd directly - kube-APIserver handles all database interactions

### kube-scheduler

- Schedules Pods onto nodes
- Evaluates individual Pod requirements and selects most suitable node
- Doesn't launch Pods - just assigns nodes to Pod objects
- Considers:
    - Node state and constraints
    - Hardware, software, and policy requirements
    - Affinity parameters (Pods that should run together)
    - Anti-affinity parameters (Pods that shouldn't run together)

### kube-controller-manager

- Continuously monitors cluster state through kube-APIserver
- Makes changes when current state doesn't match desired state
- Manages many Kubernetes objects through controller loops
- Examples:
    - **Deployment controller**: Manages workloads (like 3 nginx Pods)
    - **Node Controller**: Monitors and responds to offline nodes

### kube-cloud-manager

- Manages controllers that interact with cloud providers
- Brings in cloud features like load balancers and storage volumes

## Node Components

### kubelet

- Kubernetes agent on each node
- Receives Pod start requests from kube-APIserver
- Uses container runtime to start Pods
- Monitors Pod lifecycle (readiness/liveness probes)
- Reports back to kube-APIserver

### Container Runtime

- Software that launches containers from container images
- GKE uses containerd (Docker runtime component)
- Multiple runtime choices available in Kubernetes

### kube-proxy

- Maintains network connectivity among Pods in cluster
- Uses iptables firewalling capabilities built into Linux kernel


## Kubernetes Object Management

### Object Identification

- **Unique name**: Required for each object
- **Unique identifier (UID)**: Generated by Kubernetes for every object created

### Manifest Files

- **Purpose**: Define objects you want Kubernetes to create and maintain
- **Format**: Ordinary text files written in YAML or JSON (YAML commonly used)
- **Function**: Declare desired state for objects (name, container images, etc.)

### Required Fields in Manifest Files

- **apiVersion**: Kubernetes API version used to create the object
- **kind**: Type of object you want (e.g., Pod)
- **metadata**: Contains:
    - Object name
    - Unique ID
    - Optional namespace

### Best Practices

#### File Organization

- Define related objects in same YAML file for easier management
- Save YAML files in version-control repositories for:
    - Easier tracking and management of changes
    - Ability to undo changes when necessary
    - Cluster recreation or restoration assistance
- [[Cloud Source Repositories]] is popular service for version control

#### Object Naming Rules

- **Name requirements**:
    - Unique string under 253 characters
    - Can contain numbers, letters, hyphens, and periods
    - Only one object can have particular name at same time in same namespace
    - Names can be reused after object deletion

#### Object Organization

- **Unique Identifier (UID)**: Generated by Kubernetes for every object throughout cluster lifetime
- **Labels**: Key-value pairs for tagging objects
    - Can be applied during or after object creation
    - Help identify and organize objects

### Example Use Case

Creating three nginx web servers that run continuously:

- Declare three Pod objects specifying their state
- Each Pod must be created with nginx container image specified in manifest


## Kubernetes Operations

### kubectl Command Overview

kubectl is a utility used by administrators to control Kubernetes clusters by communicating with the Kube API server on the control plane. It allows users to make requests to the cluster and determines which part of the control plane to communicate with.

### How kubectl Works

#### Basic Operation

- Transforms command-line entries into API calls
- Sends API calls to the Kube API server
- Must be configured with location and credentials of Kubernetes cluster before use

#### Configuration Storage

- Stores configuration in hidden `.kube` folder in home directory
- Contains list of clusters and credentials for each cluster
- Credentials provided by GKE through gcloud command

#### Example Workflow

1. Administrator issues `kubectl get pod` command
2. kubectl converts command into API call
3. Sends API call to Kube API server via HTTPS on control plane
4. Kube API server processes request by querying etcd
5. Results returned to kubectl through HTTPS
6. kubectl interprets API response and displays results

### Connecting kubectl to GKE

#### Initial Setup

- Use `gcloud get-credentials` command to retrieve cluster credentials
- Available in any environment with gcloud command-line tool and kubectl installed
- Both tools installed by default in Cloud Shell

#### Configuration Process

- `gcloud get-credentials` writes configuration to `.kube/config` file in $HOME directory
- Rerunning command for different cluster updates config file with new credentials
- Only needs to be performed once per cluster in Cloud Shell
- `.kube` directory contents persist in $HOME directory

#### Tool Relationships

- **gcloud**: How authorized users interact with Google Cloud from command line
- **kubectl**: Tool for administering internal state of existing clusters
- **kubectl limitations**: Cannot create new clusters or change existing cluster shape (done through GKE control plane via gcloud/Google Cloud console)

### kubectl Syntax Structure

kubectl commands have four parts: `kubectl [COMMAND] [TYPE] [NAME] [FLAGS]`

![[kubectl-command-structure.png]]

#### COMMAND

- Specifies action to perform: `get`, `describe`, `logs`, `exec`
- Some commands show information, others change cluster configuration

#### TYPE

- Defines Kubernetes object for command to act upon
- Examples: pods, deployments, nodes, cluster
- Combined with COMMAND tells kubectl what action to perform on which object type

#### NAME

- Specifies specific object within TYPE
- Not always required, especially for listing commands
- Examples:
    - `kubectl get pods` - returns all pods
    - `kubectl get pod my-test-app` - returns specific pod

#### FLAGS

- Optional parameters appended to end of command
- Make special requests or modify output
- Examples:
    - `kubectl get pod my-test-app -o=yaml` - outputs pod state in YAML format
    - `kubectl get pods -o=wide` - displays pods in wide format showing additional info like node location

### kubectl Uses

- Creating Kubernetes objects
- Viewing objects
- Deleting objects
- Viewing or exporting configuration files

**Important**: Always configure kubectl first or use `--kubeconfig` or `--context` parameters to ensure commands execute on intended cluster.


### Introspection

Introspection is the act of gathering information about containers, pods, services, and other engines that run within the cluster to debug problems when applications are running.

#### Key Commands for Gathering Information

Four essential commands for app debugging: `get`, `describe`, `exec`, and `logs`

#### Pod Status Investigation

##### kubectl get pods

Shows whether Pod is running with phase status indicators:

- **Pending**: Kubernetes accepted Pod but still being scheduled; container images not yet created by container runtime (e.g., images being pulled from repository)
- **Running**: Pod successfully attached to node with all containers created; containers can be starting, restarting, or running continuously
- **Succeeded**: All containers finished running successfully and terminated successfully without restarting
- **Failed**: Container terminated with failure and won't restart
- **Unknown**: Pod state cannot be retrieved, usually due to communication error between control plane and kubelet
- **CrashLoopBackOff**: Container exited unexpectedly after being restarted at least once (common error indicating incorrect Pod configuration)

##### kubectl describe pod <pod_name>

Provides detailed Pod and container information including:

**Pod Information**:

- Name, namespace, node name
- Labels, status, IP address
- Resource requirements and volumes

**Container Information**:

- State (waiting, running, terminated)
- Images, ports, commands
- Restart counts

#### Container Debugging Commands

##### kubectl exec

- Runs single command inside container
- View results in your command shell
- Useful for simple commands like `ping`

**Interactive Shell**:

- Use `-it` switch to launch interactive shell
- Connects your shell to container for working inside container
- `-i`: Passes terminal's standard input to container
- `-t`: Tells kubectl input is TTY
- Without these arguments, exec command executes and returns immediately

```
kubectl exec -it my-pod -- /bin/bash
```

##### kubectl logs

- Shows what's happening inside Pod
- Reveals errors or debugging messages from applications
- Contains standard output and standard error messages
- Use `-c` argument for specific container logs in multi-container Pods
- Useful for troubleshooting containers failing to run successfully

#### Best Practices and Warnings

**Container Modification**:

- Installing software directly into containers is **not best practice**
- Container file system changes are usually ephemeral
- Use interactive shell to identify needed changes
- Integrate changes into container images and redeploy
- Build container images with exactly the software needed rather than temporary runtime repairs
