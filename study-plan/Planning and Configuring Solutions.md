
## Topics

### Planning and Configuring Compute Resources

There are five distinct ways to interact with compute resources in Google Cloud. They can be divided into server-based services, where manage and pay for infrastructure, and serverless options, where you just pay for execution time.

#### Server-based Services

[[Compute Engine]] and [[Google Kubernetes Engine]] are server-based. All of these services abstract the underlying infrastructure away so you can focus on code. You only pay for how long the application runs.

[[Compute Engine]] is Google Cloud’s [[IaaS|infrastructure-as-a-service]] offering. It gives you maximum flexibility of developing on a virtual machine (VM). It does require more management than serverless options, though.

A VM has an operating system. You choose how and if it autoscales. Autoscaling can add more machines based on monitored performance thresholds. 

A common use case for Compute Engine is migrating an enterprise application designed to run on a server infrastructure. If you set up an architecture similar to your on-premise solution you can port your code quite easily. 

To monitor performance you can connect Cloud Logging and Monitoring from [[Google Cloud Observability]].

[[Google Kubernetes Engine|GKE]] is a platform-as-a-service offering for running containerized applications in the cloud. Google manages the control plane for you, under your administrative control. Containers abstract application dependencies from the host operating system. This makes container architectures highly portable. It saves costs compared to implementing multiple VMs on a host hypervisor, which each requiring a copy of the operating system. Kubernetes lets you orchestrate code in containers.

If you have containerized applications that use a native Kubernetes architecture in your on-premise environment, it can be straightforward to migrate to Google Cloud.
#### Serverless Options

[[App Engine]], [[Cloud Run]], and [[Cloud Run Functions]] are serverless options, where you focus on code and Google manages the underlying hardware and operating system for you. In Compute Engine you implement and manage virtual machines that your apps run on. With GKE you implement and manage clusters of compute nodes you deploy your container images to.

[[App Engine]] has two environments: standard and flexible. Standard provides a sandbox environment and totally abstracts the infrastructure for you. The flexible environment gives you more choices for deploying your app. It supports more languages, supports different runtimes, and lets you load dependencies you need in the underlying architecture.

[[Cloud Run]], which is also serverless, enables you to run stateless containers via web requests and Google Cloud service events. Cloud Run operates using Knative, an open-source, Kubernetes-based platform. It builds, deploys, and manages modern serverless workloads. [[Cloud Run]] gives you the choice of running your containers either fully-managed or in your own GKE cluster.


#### Where To Look

https://cloud.google.com/blog/products/compute/choosing-the-right-compute-option-in-gcp-a-decision-tree

https://cloud.google.com/hosting-options

https://cloud.google.com/compute/docs/tutorials

https://cloud.google.com/docs/choosing-a-compute-option

#### Content Mapping

- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M3 Virtual Machines and Networks in the Cloud
	- M5 Containers in the Cloud
	- M6 Applications in the Cloud
	
- [Getting Started with Google Kubernetes Engine (On-demand)](https://www.cloudskillsboost.google/course_templates/2)

- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M2 Introduction to Containers and Kubernetes 
	- M3 Virtual Machines

- [Essential Google Cloud Infrastructure: Foundation (On-demand)](https://www.cloudskillsboost.google/course_templates/50)
	- M3 Virtual Machines

- Skill Badge
	- [Develop your Google Cloud Network](https://www.cloudskillsboost.google/course_templates/625)


### Planning and Configuring Data Storage

Two common workloads required in a modern business environment are transactional workloads and analytical workloads. 

#### Transactional vs Analytical

Transactional workloads are optimized for more writes and updates than reads. Transactional means either all parts of an update happen or none of them do. For example, think of the importance of making sure deposits and withdrawals are recorded in a financial system. Both of these are part of one transaction.

The other type of workload is analytical. It is based on querying historical data that doesn’t change often, and is optimized for reads.

#### Relational

Relational database management systems are commonly used for applications that are transactional in nature. 

Google’s relational database offerings include [[Cloud SQL]] and [[Cloud Spanner|Spanner]]. Use them when you need a transactional processing system you can query with SQL. Cloud SQL is a managed version of databases you can implement on-premises, while Spanner is horizontally scalable and globally available.

#### Analytical

[[BigQuery]] is a serverless distributed query engine that is primarily used as a modern data warehouse. It does have a native storage format but can also query external data where it resides. You interact with it by using a form of SQL. Keep in mind its native storage format is not a good solution for a backend store for an application. It does, however, improve performance of analytical queries you run against it using the query engine.

#### NoSQL

[[Firestore]] and [[Bigtable]] are NoSQL implementations. [[Firestore]] is a document database that supports entities and attributes. [[Bigtable]] is based on column families where rows of data are referenced by a key that combines commonly queried columns. Related columns can additionally be organized into column families such as username and address.

### Storage

[[Cloud Storage]] is Google Cloud’s recommended object storage service. Think of pictures and videos, as well as file objects with an implicit schema, such as logs and csv files.

##### Storage Classes

Data location and storage class affect the availability and cost of storing your data in Cloud Storage. You can choose regional, dual-region, and multi-regional location options. Storage classes include Standard, Nearline, Coldline and Archive storage. The different storage classes determine pricing based on how long your data is stored and how often you access it. 

Standard storage is the default storage class. Data stored using this class is immediately available. It is the recommended storage class for frequently accessed data. You should locate your data in the same region as the services you are going to use to ingest and analyze the data to reduce latency as much as possible. Specifying a dual-region location that includes the region where your application resides will still give you low latency, but your data will also be available in another region in case of an outage. Extending your storage settings to a multi-region will make data available over a large geographic area such as US, Europe, or Asia. 

The other storage classes implement ways to store infrequently accessed data. Nearline storage is for data that is only accessed around every 30 days. Coldline storage is for data that is only accessed around once every quarter, or 90 days. Archive storage is long-term storage for data accessed only once a year. These storage classes have optimized pricing, but also expect you to keep your data in them for the minimum limits specified above. If you access your data before the minimum amount of time you will be charged a data access fee

#### Where To Look

https://cloud.google.com/storage-options/

https://cloud.google.com/storage/docs/storage-classes

#### Content Mapping

- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M4 Storage in the Cloud

- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M5 Storage and Database Services

- [Essential Google Cloud Infrastructure: Core Services (On-demand)](https://www.cloudskillsboost.google/course_templates/49)
	- M2 Storage and Database Services

- Skill Badge
	- [Set Up and App Dev Environment on Google Cloud](https://www.cloudskillsboost.google/course_templates/637)


### Planning and Configuring Network Resources

Google Cloud offers a range of load balancing solutions that can be classified based on the OSI model layer they operate at and their specific functionalities.

#### Application Load Balancers

These load balancers operate at the application layer and are designed to handle HTTP and HTTPS traffic, making them ideal for web applications and services that require advanced features like content-based routing and SSL/TLS termination. Application Load Balancers operate as reverse proxies, distributing incoming traffic across multiple backend instances based on rules you define. They are highly flexible and can be configured for both internet-facing (external) and internal applications.

The Application Load Balancer is a proxy-based Layer 7 load balancer that lets you run and scale your services. The Application Load Balancer distributes HTTP and HTTPS traffic to backends hosted on a variety of Google Cloud platforms—such as Compute Engine, Google Kubernetes Engine (GKE), Cloud Storage, and Cloud Run—as well as external backends connected over the internet or by using hybrid connectivity.

#### Network Load Balancers

Network Load Balancers operate at the transport layer and efficiently handle TCP, UDP, and other IP protocols. They can be further classified into two types: 

Proxy Load Balancers: These also function as reverse proxies, terminating client connections and establishing new ones to backend services. They offer advanced traffic management capabilities and support backends located both on-premises and in various cloud environments. 

Passthrough Load Balancers: Unlike proxy load balancers, these do not modify or terminate connections. Instead, they directly forward traffic to the backend while preserving the original source IP address. This type is well-suited for applications that require direct server return or need to handle a wider range of IP protocols.

#### Where To Look

https://cloud.google.com/load-balancing/docs/load-balancing-overview

#### Content Mapping

- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M3 Virtual Machines and Networks in the Cloud
	
- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M2 Virtual Networks
	- M9 Load Balancing and Autoscaling

- [Essential Google Cloud Infrastructure: Foundation (On-demand)](https://www.cloudskillsboost.google/course_templates/50)
	- M2 Virtual Networks

- [Essential Google Cloud Infrastructure: Core Services (On-demand)](https://www.cloudskillsboost.google/course_templates/49)

- [Elastic Google Cloud Infrastructure: Scaling and Automation (On-demand)](https://www.cloudskillsboost.google/course_templates/178)
	- M2 Load Balancing and Auutoscaling 


