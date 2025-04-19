
## Objectives

- Identify purpose of Google Cloud products and services
- Define how infrastructure is organized and controlled in Google Cloud
- Explain how to create a basic infrastructure in Google Cloud
- Select and use Google Cloud storage options
- Describe the purpose and value of Google Kubernetes Engine
- Identify the use cases for serverless Google Cloud services
- Combine Google Cloud knowledge with prompt engineering to improve Gemini responses


## Introducing Google Cloud

### Overview

#### Cloud Computing
- Customer get resources that are on-demand and self-service
- Access to resources over the internet - connect from anywhere
- Cloud provider has big pool of resources and allocates them from pool
- Resources are elastic
- Pay for what you use

### Trend Toward Cloud
- Co-location - first wave
- Virtualized data centers - second wave
- Container based architecture

### [[IaaS]] and [[PaaS]] and [[SaaS]]

- IaaS - customer pays for resources they allocate ahead of time
- PaaS - customer pays for resources they actually use
- SaaS - entire application stack delivered as cloud-based application

### Google Cloud Network

- More than 100 content caching nodes worldwide
- Geographic locations in North America, South America, Europe, Asia, Australia
- Each location divided into regions, which are independent geographic areas comprised of zones
- Some services support being placed in multi-region
- Most up-to-date numbers at cloud.google.com/about/locations

### [[Sustainability]]


### Security

#### Hardware Infrastructure Layer
- Google custom designed server boards and networking
- Secure boot stack ensure booting correct software stack - cryptographic signatures over BOIS, bootloader, kernel, OS image
- Premises are physically secure - own datacenters with multiple layers of security, limited access, and in third party data centers there are Google controlled security measures

#### Service Deployment Layer

- Encryption of inter-service communication

#### User Identity Layer

- Google central identity service
- 2FA / MFA - Universal 2nd Factor (U2F) open standard
- Intelligently challenge users based on risk profile

#### Storage Services Layer

- Encryption at rest
- Hardware encryption support in hard drives and SSDs

#### Internet Communication Layer

- Google Front End - infrastructure service for all internet facing services that ensures TLS connections in place with X.509 certificates
- Denial of Service protection  - scale enables Google to absorb attacks, plus multiple layers of protection to further reduce risk

#### Operation Layer

- Intrusion detection - rules plus ML intelligence to detect anomalies
- Red Team exercises - simulate attacks to test defenses
- Reduce insider risk - least privilege access, monitoring, and auditing, and U2F security keys for Google employees - guard against phishing attacks
- Stringent software development practices - central source control with two-party reviews of new code, libraries that prevent certain types of bugs, Vulnerability Rewards Program where payment is made for finding bugs in infrastructure or applications

#### Learn More
cloud.google.com/security/security-design


### Open Ecosystems

- Google publishes key elements of technology using open source licenses to create ecosystems that provide customers with options other than Google.
	- e.g. TensorFlow - of open source machine learning library
- Interoperability - Google Cloud is designed to work with other cloud providers and on-premises environments
	- e.g. Kubernetes and [[Google Kubernetes Engine|GKE]] provide ability to mix microservices across different clouds
	- e.g. [[Google Cloud Observability]] - provides visibility into applications running on Google Cloud and other cloud providers

### Pricing and Billing

- Per second billing for IaaS compute offering [[Compute Engine]], [[Google Kubernetes Engine|GKE]], [[Dataproc]] and [[App Engine]]
- Automatically applied sustained use discounts for [[Compute Engine]] - kicks in after 25% of month
- [Online pricing calculator](cloud.google.com/products/calculator) helps estimate costs
- Budgets at billing account and project level to help manage costs with alerts when approaching limits - usually set a 50%, 90% and 100% thresholds but can be customized
- Quotas to prevent overuse of resources and malicious attacks
	- Rate quotas - reset after specific time, e.g. max 3000 requests to [[Google Kubernetes Engine|GKE]] APIs every 100 seconds
	- Allocation quotas - govern number of resources that can be created in projects - e.g. projects default to a max of 15 [[Virtual Private Cloud|VPC]] networks


## Resources and Access in the Cloud

### [[Google Cloud Resource Hierarchy]]

### [[Identity and Access Management (IAM)]]

### [[Service Accounts]]

### [[Cloud Identity]]

### [[Interacting with Google Cloud]]


## Virtual Machines and Networks in the Cloud

### [[Virtual Private Cloud]]

### [[Compute Engine]]



## Storage in the Cloud

### [[Cloud Storage]]

### [[Cloud SQL]]

### [[Cloud Spanner]]

### [[Firestore]]

### [[Bigtable]]

### [[BigQuery]]

### Choosing a Storage Option

Depending on requirements, one or multiple of the following storage options can be used:

- Cloud Storage
	- Storing immutable blobs larger than 10 MB
	- Capacity: Petabytes, Max unit size 5 TB per object
- Cloud SQL
	- Full SQL support for online transaction processing
	- Web frameworks and existing applications
	- Capacity: Up to 64TB
- Spanner
	- Full SQL support for online transaction processing system
	- Horizontal scalability
	- Capacity: Petabytes
- Firestore
	- Massive scaling and predictability with real time query results and offline query support
	- Best for storing, syncing and querying data for mobile and web apps
	- Capacity: Terabytes, 1 MB per entity
- Bigtable
	- Storing large number of structured objects
	- Does not support SQL queries or multi row transactions
	- Best for analytical data with heavy read/write events like AdTech, financial or IoT data
	- Capacity: Petabytes, Max unit size 10 MB per cell, 100 MB per row
- BigQuery
	- Sits on edge between data storage and data processing, not purely a storage solution
	- Best for data analysis and interactive querying capabilities


## Containers in the Cloud

A container is an invisible box around your code and its dependencies with limited access to its own partition of the file system and hardware.
- Only requires an OS kernel that supports containers and container runtime
- Scales like PaaS but gives nearly same flexibility as IaaS
- Makes code ultra portable, OS and hardware can be treated as black box

### Kubernetes

- Open source container orchestration system
- Orchestrate many containers on many hosts, scale them as microservices, deploy rollouts and rollbacks
- Provides set of APIs for deploying containers on clusters.
- Divided into primary components that run as control plane, and set of nodes that run as containers.
- A Node represents a compute instance like a machine.
- Describe a set of applications and how they should interact, and Kubernetes will deploy and manage them.
- A Pod is the smallest unit in Kubernetes that can be created or deployed, and represents a running process on your cluster.
- Generally one container per Pod, but multiple containers with hard dependencies can be packaged into a single Pod. Can share network and storage resources.
- Pod provides unique network IP and set of ports and config options for how container should run.
- A Deployment represents a group of replicas of same Pod, keeps Pods running even when the nodes they run on fail. Can use `kubectl run` command to start a Deployment. To list running Pods, run the `kubectl get pods` command.
- Deployments can be scaled using `kubectl scale` command, or autoscaling can be used based on parameters like CPU usage or memory usage.
- As Deployments create and destroy Pods, they will be assigned new IP addresses. To access a Pod, you need to use a Service.
- A Service is an abstraction that defines a logical set of Pods and a policy by which to access them. Can be used to expose an application running on a set of Pods. Services have a fixed IP address for Pods, and controller attaches external load balancer with public IP address to a Service.
- In [[Google Kubernetes Engine|GKE]] the load balancer is a network load balancer. Any client that reaches IP will be routed to Pod behind a Service.
- Deployment config file proved declarative way to describe how to deploy application. Can be used to create a Deployment using `kubectl apply` command.
- Updates can be applied using `kubectl rollout` command, or change the Deployment config file and reapply it.


## Applications in the Cloud

### [[Cloud Run]]

## [[Cloud Run Functions]]


## Prompt Engineering

### Generative AI
A broad range of models capable of generating various types of content beyond just text.

### LLM
Subset of generative AI models focusing on language tasks.

### Gemini
- Gemini is a large language model (LLM) developed by Google DeepMind.
- Embedded in many Google Cloud products with access to a range of data including Google Cloud documentation, tutorials and samples.

### Prompts
- Text fed to the model, which can be a question or instruction. Better articulated (engineered) prompts lead to better responses from the model.

#### Zero Shot
Prompt that does not contain any context or examples to assist the model
```
What is the capital of France?
```

#### One-Shot
Prompt that contains a single example to assist the model
```
Tell me the capital of the country.
Italy: Rome
France: ___________
```

#### Few-Shot
Prompt that contains multiple examples to assist the model
```
Tell me the capital of the country.
Italy: Rome
Japan: Tokyo
France: ___________
```

#### Role Prompts
Prompt that specifies a role for the model to play
```
I want you to act as a business professor. I’ll give you a term, and you will correctly explain its meaning. Make sure your answers are always right. What is ROI?
```

### Elements of Prompt

#### Preamble
Introductory text you provide to give the model context and instructions before your main question or request. Setting the stage.
- Context
- Instruction / task
- Examples - one-shot or few-shot

#### Input
The central request made to the LLM. 

#### Example

##### Context
```
VideoS is a video platform where users can add short comments. Comments can be positive, neutral, negative.
```

##### Instruction/task
```
You need to classify the comments as positive, neutral, negative. Here are some examples:
```

##### Examples
```
Comment: This video is awful.
The review is: Negative

Comment: No opinions about it.
The review is: Neutral

Comment: Loved it!
The review is: Positive
```

##### Input
```
Comment: I don't know what to think about the video.
The review is: 
```


#### Example for Google Cloud

```
I want you to act as a cloud architect in Google Cloud. How can I use gcloud to create a network that uses IPv4 and IPv6 subnets?
```

#### Best Practices

- Be clear and concise
- Define boundaries
- Better to instruct the model on what to do rather than what not to do
- If model gets stuck, give it a few fallback outputs that work in various situations
	- e.g. something like `"I'm still learning about that"` to use if unsure.
- Adopt a persona for your input - can provide context to help focus on related questions to improve accuracy.
- Use short sentences. Longer sentences can produce suboptimal results.
- Break long sentences into series of shorter sentences and simpler tasks.

```
You are a cloud architect. You want to build a Google Cloud VPC network that can be centrally managed. You also connect to other VPC networks in your company's other regions. You don't want to have many different sets of firewall policies to maintain. What sort of network architecture would you recommend?
```



