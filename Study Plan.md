
![[study-plan.png]]

## [[Setting Up a Cloud Solution Environment]]

- Create resource hierarchy
- Apply organizational policies
- Grant members [[Identity and Access Management (IAM)|IAM]] roles withing a project
- Manage users and groups in [[Cloud Identity]]
- Enable APIs within projects
- Provision and set up products in [[Google Cloud Observability]]
- Billing management and quotas and requesting increases

## [[Planning and Configuring Solutions]]

### Considerations
- Compute options
	- VM / Container / Serverless
- Data solutions
	- Throughput and latency will determine performance
	- Data processing transactional or analytical?
	- Is relational querying required?
	- Large groups of data returned in non relational get operation?
- Network connectivity
	- Internet connectivity?
	- Private network connectivity?
	- Network or system outage mitigation strategies

## [[Deploying and Implementing Solutions]]

- Availability, concurrency, connectivity and access options
- Data solutions that utilize relational or NoSQL databases
- Use cases for transactional or analytical data processing
- Deploying infrastructure in a declarative way
- Infrastructure as code to reduce human error
- Interacting via Cloud console, command line or programmatically (API)

## [[Ensuring Successful Operation of a Cloud Solution]]

- Managing Compute Engine Resources
	- Remotely connecting to instances
	- Viewing current running VM inventory (instance IDs, details)
	- Working with VM snapshots (create, view, delete, schedule VM snapshots)
	- Working with images (create image from VM / snapshot, view images, delete image)
- Managing [[Google Kubernetes Engine]] Resources
	- Viewing current running cluster inventory (e.g. nodes, pods, services)
	- Configure [[Google Kubernetes Engine|GKE]] to access [[Artifact Registry]]
	- Working with node pools (e.g. add, edit, remove node pool)
	- Working with Kubernetes resources (e.g. Pods, StatefulSets, Deployments, Services)
	- Managing Horizontal and Vertical autoscaling configurations
- Managing Cloud Run Resources
	- Deploying new versions of an application
	- Adjusting application traffic splitting parameters
	- Setting scaling parameters for autoscaling instances
- Managing Storage and Database Solutions
	- Managing and securing objects in Cloud Storage buckets
	- Setting object lifecycle management policies for Cloud Storage buckets
	- Executing querires to retrieve data from data instances (e.g. BigQuery, Cloud SQL, Firestore, Spanner, AlloyDB)
- Managing Networking Resources
	- Adding a subnet to a VPC network
	- Expanding a subnet to have more IP addresses
	- Reserving a static external IP address or a static internal IP address
	- Working with Cloud DND and Cloud NAT 
- Monitoring and Logging
	- Creating Cloud Monitoring alerts based on resource metrics
	- Creating and ingesting Cloud Monitoring custom metrics (e.g. from applications or logs)
	- Exporting logs to external systems (e.g. on-premises, BigQuery)
	- Configuring log buckets, log analytics, and logs routers
	- Viewing and filtering logs in Cloud Logging
	- Viewing specific log message details in Cloud Logging
	- Using cloud diagnostics to research an application issue
	- Viewing Google Cloud status
	- Configuring and deploying Ops Agent
	- Deploying Managed Service for Prometheus
	- Configuring audit logs


## [[Configuring Access and Security]]

- Managing Identity and Access Management (IAM)
	- Viewing and creating IAM policies
	- Managing the various role types and defining custom IAM roles (e.g. basic, predefined, custom)
- Managing Service Accounts
	- Creating a service account
	- Using service accounts in IAM policies with minimum permissions
	- Assigning service accounts to resources
	- Managing IAM of a service account
	- Managing service account impersonation
	- Creating and managing short-lived service account credentials

