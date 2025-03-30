
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


