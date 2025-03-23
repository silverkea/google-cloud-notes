
## Topics

### Deploying and Implementing Compute Engine Resources

[[Compute Engine]] allows you to pick the amount of memory and CPU from predefined machine types. Machine types are divided into standard, high memory, high cpu, memory-optimized, compute-optimized or shared-core categories. If none of these meet your needs, you can also create a VM with the specific resources you need. 

If you need GPU support for a compute-heavy workload, you can choose to attach GPUs to certain machine types. You can only use GPUs with general-purpose N1 VMs or accelerator-optimized A2 VMs. Availability of these machine types varies by zone, so make sure you pick a zone that has GPU capability.

Storage options for your instances include zonal persistent disks, regional persistent disks, and local SSD. Persistent disks are built on network storage devices that are separate from the physical hardware your instance is running on.

Each persistent disk references data distributed across several physical disks. Regional persistent disks share replicas of the physical disks across two zones, so you are protected from a single zone outage. Disk types you can attach to your virtual machine include standard (HDD), SSD, or local SSD. When you create a virtual machine instance in the console it uses balanced SSD, while when you create one via a gcloud command, it uses standard HDD. Balanced SSD gives you higher I/O than standard HDD, but less cost and I/O than fully capable SSD disks.

Local SSDs can be added to your instances based on machine type. They provide very high I/O since they are physically connected to the server your VM is running on. They are ephemeral, and thus go away when your VM is stopped or terminated. Data on your local SSD will survive a reboot. You are responsible for formatting and striping the local SSD per your requirements.

##### Availability
A managed instance group ensures availability by keeping VM instances running. If a VM fails or stops, the MIG recreates it based on the instance template. You can make your MIG health checks application-based, which looks for an expected response from your application. The MIG will automatically recreate VMs that are not responding correctly. Another availability feature is spreading load across multiple zones using a regional MIG. Finally, you can use a load balancer to evenly distribute traffic across all instances in the group.

##### Scalability
You can define autoscaling policies to grow instances in the group to meet demand. They can also scale back down when load drops which reduces cost.

##### Automated updates
when it comes time to update software, automated updates lets you define how you will upgrade the instances in a group. You can specify how many resources to use and how many instances can be unavailable at the same time. Available update scenarios include rolling updates and canary updates. Rolling updates define how you want all instances eventually upgraded to the new template. Canary updates let you specify a certain number of instances to upgrade for testing purposes.

#### Where to Look
https://cloud.google.com/compute/docs/
https://cloud.google.com/compute/docs/instance-groups/creating-groups-of-managed-instances

#### Content Mapping

- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M3 Virtual Machines and Networks in the Cloud

- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M3 Virtual Machines
	- M9 Load Balancing and Autoscaling
	- M10 Infrastructure Automation

- [Essential Google Cloud Infrastructure: Foundation (On-demand)](https://www.cloudskillsboost.google/course_templates/50)
	- M3 Virtual Machines

- [Elastic Google Cloud Infrastructure: Scaling and Automation (On-demand)](https://www.cloudskillsboost.google/course_templates/178)
	- M2 Load Balancing and Autoscaling
	- M3 Infrastructure Automation


### Deploying and Implementing Google Kubernetes Engine Resources

##### Mode
GKE has to modes to choose from: autopilot mode and standard mode. Autopilot is fully-provisioned and managed. You are charged according to the resources pods use as you deploy and replicate them based on the pod spec. Standard mode provides you flexibility to define and manage the cluster structure yourself.

##### Availability
In a GKE cluster, availability deals with both the control plane and the distribution of your nodes. A zonal cluster has a single control plane in a single zone. You can distribute the nodes of a zonal cluster across multiple zones, providing node availability in case of a node outage. A regional cluster, on the other hand, has multiple replicas of the control plane in multiple zones with a given region. Nodes in a regional cluster are replicated across three zones, though you can change this behavior as you add new node pools.

##### Version
At setup you can choose to load a specific version of GKE or enroll in a release channel. If you don’t specify either one of those, the current default version is chosen. It is a best practice to enable auto-upgrade for cluster nodes and the cluster itself.

##### Network Routing
Routing between pods in GKE can be accomplished using alias IPs or Google Cloud Routes. The first option is also known as a VPC-native cluster, and the second one is called a routes-based cluster.

##### Network Isolation
Public GKE networks let you set up routing from public networks to your cluster. Private networks use internal addresses for pods and nodes and are isolated from public networks.

##### Features
Cluster features for Kubernetes will be either Alpha, Beta, or Stable, depending on their development status.

#### Where To Look

https://cloud.google.com/kubernetes-engine/docs/concepts/types-of-clusters

#### Content Mapping

- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M5 Containers in the Cloud

- [Getting Started with Google Kubernetes Engine (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/2)
	- M2 Introduction to Containers and Kubernetes
	- M3 Kubernetes Architecture

- Skill Badge
	- [Develop your Google Cloud Network](https://www.cloudskillsboost.google/course_templates/625)


### Deploying and Implementing Cloud Run and Cloud Run Functions resources

##### Cloud Run
Cloud Run provides a service to manage containers in a serverless way, which means you don’t need to manage infrastructure when you deploy an application. The main resource container for Cloud Run is a service. A service is a regional resource that is replicated in multiple zones and exposed as an endpoint. Underlying infrastructure scales automatically based on incoming requests. If there are no requests coming in it can scale to zero to save you money.

Changes to containers or environment settings create new revisions. Revisions can be rolled out in a way that supports canary testing by splitting traffic according to your specifications.

Cloud Run is built using an open source initiative called knative. It is billed to the nearest 100 MS as you deploy containers to it.

Cloud Run can use system libraries and tools made available to the container environment. It has a timeout of 60 minutes for longer running requests. Cloud Run can send multiple concurrent requests to each container instance, improving latency, and saving costs for large volumes of incoming traffic.

##### Cloud Run Functions
Cloud Run functions is Google Cloud’s answer to serverless functions. It is a fully managed service based on events that happen across your cloud environment, including services and infrastructure. The functions you develop run in response to those events. There are no servers to manage or scaling to configure. The service provides the underlying resources required to execute your function.

A trigger sends an https request to an endpoint the service is listening on. This endpoint then responds by deploying and executing the function and returning the results specified in your code. Pricing is based on the number of events, compute time, and memory required in network ingress/egress. If no requests are coming in, your function doesn’t cost anything.

Cloud Run functions use cases include IoT processing and lightweight ETL.

Depending on the programming language you choose, the Cloud Run functions service provides a base image and runtime that will be updated and patched automatically. This helps keeps execution of your deployed functions secure.

By design, functions you write for use by the Cloud Run functions service are stateless. If you need to share and persist data across function runs, you should consider using Datastore or Cloud Storage. Each Cloud Run function instance handles only one concurrent request at a time. If, while handling a request, another one comes in, Cloud Run functions will ask for more instances to be created. This is another reason functions need to be stateless, because they can run on different instances. You can implement minimum instance limits to avoid latency associated with cold starts.

##### App Engine
Another traditional serverless application manager available in Google Cloud is App Engine. App Engine has two management environments: standard and flexible.

In the standard environment, apps run in a sandbox using a specific language runtime. Standard environment is good for rapid scaling. It is limited to specific languages. It can scale to 0 when there is no incoming traffic. It starts up in seconds. In the standard environment you are not allowed to make changes to the runtime.

In contrast to the standard environment, App Engine flexible runs in Docker containers in Compute Engine VMs. Flexible supports more programming languages. It can use native code and you can access and manage the underlying Compute Engine resource base.

App Engine flexible does not scale to 0. Startup is in minutes. Deployment time is in minutes (longer than standard). It does allow you to modify the runtime environment.

#### Where To Look
https://cloud.google.com/appengine/docs/the-appengine-environments
https://cloud.google.com/hosting-options
https://cloud.google.com/blog/topics/developers-practitioners/cloud-run-story-serverless-containers
https://cloud.google.com/functions
#### Content Mapping

- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M6 Applications in the Cloud
	- M7 Developing and Deploying in the Cloud


### Deploying and Implementing Data Solutions

##### Cloud Storage
Cloud Storage helps you store binary objects in Google Cloud. It can house data in any format as an immutable object. In Cloud Storage, objects are stored in containers called buckets.

Buckets can be used to upload and download objects, and permissions can be assigned to specify who has access to them.

You can manage and interact with Cloud Storage via the console, via the command line and the `gcloud` storage command set, via client libraries, or through APIs. Steps for creating a cloud bucket include:

- Naming your bucket - has to be globally unique, and not contain any sensitive information
- Choose location type and option: 
	- Regional is a specific geographical area where a datacenter campus resides. It minimizes latency and network bandwidth for consumers grouped in a specific region 
	- Dual-region is a a specific pair or regions. It provides geo-redundancy 
	- Multi-region is a disbursed geographic area, such as the US or Europe. You can use it to serve content to consumers outside of Google and
- Pick a default storage class for bucket. You can override this per object. 
	- Standard is for immediate access and has no minimum storage duration 
	- Nearline has a 30 day minimum duration and data retrieval charges 
	- Coldline has a 90 day min duration and data retrieval charges
	- Archive has a 365 day min duration and data retrieval charges
- Click Create or submit the command

##### Cloud SQL

Cloud SQL is a Google Cloud service that manages a database instance for you. You are responsible for how you structure your data within it. Cloud SQL can handle common database tasks for you, such as automating backups, implementing high availability, handling data encryption, updating infrastructure and software, and providing logging and monitoring services. You can use it to deploy MySQL, PostgreSQL, or SQL Server databases to Google Cloud. It uses persistent disks attached to underlying Compute Engine instances to house your database, and implements a static IP address for you to connect to it.

Steps for setting up a Cloud SQL instance: 
1. Create Instance. 
2. Select database type. 
3. Enter name: do not use sensitive or personally identifiable information. Your instance name can be publicly available. 
4. Enter password for root user. 
5. Select proper version: choose carefully, it cannot be edited. 
6. Regional and zonal availability settings. Can’t be modified. Pick a region where most people will access. You can also choose multi-region. 
7. Select both primary and secondary zone. Both default to any with secondary being different than the primary. 
8. Config settings include machine type, private or public ip, storage type, storage capacity, threshold for automated storage increase, as well as an increase setting to specify a limit on how big your database grows.

##### BigQuery Batch Load

BigQuery offers several ways to load data. The first, and oldest, is loading data in batch. Batch loading is done in a single operation. It can be used to load data from csv files, databases, and log files. Batch loading is often used when you need to ingest files from your local computer. It is the recommended way to load slowly changing data. There is no charge for batch loads into BigQuery.

The ways you can implement a batch load in BigQuery include: 
1. Create a load job. 
2. Use BigQuery Data Transfer Service from Software as a Service products. This is the simplest approach. 
3. Use Cloud Composer, a Google Cloud managed version of Apache Airflow. 
4. Use the bq command line tool and the cron scheduler on the command line interface. 
5. Use BigQuery connectors for big data products such as Spark or Hadoop.

For real-time use cases you can stream data into BigQuery using the Streaming API. Data streamed into BigQuery can be used for querying immediately. The streaming API can be used to track and query application events or log stream information.

The third way to ingest data into BigQuery is to use Dataflow and Apache Beam. These two technologies define a processing pipeline where your source or sink can be BigQuery. A possible use-case for this is to trigger a Cloud Run function when an event happens. The Cloud Run function could contain the logic to start an Apache Beam pipeline using a Dataflow runner that would execute transformations required and then save your data into BigQuery when it is done.

Another way to load data is to execute queries in BigQuery native storage or federated queries on external data and save the results to a table. CTAS (create table as select) is a way to do this using DML as well.

Finally, many third party applications have connectors you can use to get data in to BigQuery. You would need to look at the documentation of the product you want to ingest data from.

#### Where To Look

https://cloud.google.com/storage/docs/creating-buckets
https://cloud.google.com/storage/docs/introduction
https://cloud.google.com/sql/docs/mysql/features
https://cloud.google.com/sql/docs/mysql/create-instance
https://cloud.google.com/blog/topics/developers-practitioners/bigquery-explained-data-ingestion
https://cloud.google.com/bigquery/docs/loading-data

#### Content Mapping

- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M4 Storage in the Cloud
	
- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M5 Storage and Database Services

- [Essential Google Cloud Infrastructure: Core Services (On-demand)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M2 Storage and Database Services

- Skill Badge
	- [Set Up an App Dev Environment on Google Cloud](https://www.cloudskillsboost.google/course_templates/637)
	- [Develop your Google Cloud Network](https://www.cloudskillsboost.google/course_templates/625)


### Deploying and Implementing Networking Resources

#### Virtual Private Clouds
Virtual private clouds are part of Google’s software defined network environment. VPCs provide connectivity to Compute Engine instances. They offer internal TCP/UDP load balancing systems. They allow you to implement Cloud VPN tunnels to communicate with your on-premises network, and they distribute external traffic to backend servers.

There are two types of network configurations that are available when you decide to create a new VPC.

##### Auto Mode
Auto mode networks create one subnet in each region automatically. New subnets are added automatically when new regions come on line. IP addresses are created from a predetermined set of address spaces. The default VPC created when you create a project is an auto mode VPC.

The benefits of using auto mode include being easy to set up and use and subnets are created in each region. You need to ensure IP ranges do not overlap with on-premise resources.

##### Custom Network
The other kind of network is a custom network. When you create a custom network, you create and configure the subnets you want and only in the regions you want. If you try to create instances in a region that doesn’t have a subnet defined, you will get an error message. Custom networks are recommended for production environments. Custom networks are a good choice when you don’t need subnets in every region.

You can convert an auto mode to a custom network, but not the reverse.

#### Where To Look

https://cloud.google.com/vpc/docs/vpc

#### Content Mapping

- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M2 Virtual Networks

- [Essential Google Cloud Infrastructure: Foundation (On-demand)](https://www.cloudskillsboost.google/course_templates/50)
	- M2 Virtual Networks

- Skill Badge:
	- [Develop your Google Cloud Network](https://www.cloudskillsboost.google/course_templates/625)


### Implementing Resources through Infrastructure as Code

Terraform is an open source tool for implementing resources in a declarative way. You specify a Terraform config file that describes the resources you want to deploy. Terraform is known as an infrastructure as code service. A benefit of implementing resources in this way is that your configuration files can be source controlled, thus following devops best practices.

In Google Cloud, you store your Terraform config files in a Cloud Storage bucket with object versioning enabled. Cloud Build submits Terraform commands via a YAML file. It needs access to the Cloud Storage bucket where your Terraform config files are stored.

The different files required for implementing Terraform in Google Cloud include:

- Cloudbuild.yaml - build configuration file that contains instructions for Cloud Build 
- Backend.tf - stores remote Terraform state information 
- Terraform.tfstate - local file that stores Terraform state 
- Main.tf - contains the terraform config

Command ran by Cloud Build include:

- Terraform init - downloads latest version of Terraform provider 
- Terraform plan - verifies syntax, ensures supporting files exist, shows a preview of resources that will be created 
- Terraform apply - sets up requested resources output by the Terraform plan 
- Terraform destroy - destroy all resources in the specified config file

#### Where To Look

https://www.terraform.io/intro/index.html
https://cloud.google.com/docs/terraform

#### Content Mapping

- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M10 Infrastructure Automation

- [Elastic Google Cloud Infrastructure: Scaling and Automation (On-demand)](https://www.cloudskillsboost.google/course_templates/178)
	- M3 Infrastructure Automation

- Skill Badge
	- [Build Infrastructure with Terraform on Google Cloud](https://www.cloudskillsboost.google/course_templates/636)
