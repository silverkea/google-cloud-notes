
## Topics

### Managing Compute Engine Resources

#### Snapshots
Snapshots are incremental in nature and less expensive than creating full images of a disk. You can only create them for persistent disks.

They are stored in a Cloud Storage bucket managed by the snapshot service and are automatically compressed. You can choose regional or multi-regional storage, which will affect cost.

Snapshots are stored across multiple locations with automatic checksums. You schedule them using the gcloud command line and cron. You can also set up a snapshot schedule in the Google cloud console or command line.

A Snapshot schedule and its source persistent disk have to be in the same region. You can restore them to a new persistent disk. The new disk can be in a different zone or region, so you can use snapshots to move VMs. You can create them while they are running. Snapshots of a disk have to be at least 10 minutes apart.

Here’s how the incremental nature of snapshots works:
- The first snapshot is a full snapshot of the disk
- Subsequent snapshots only store the changes since the last snapshot
- Sometimes to clean up resources and cost, a new snapshot might be a full backup

Deleting a snapshot copies its data to downstream incremental snapshots that are dependent on it, increasing the downstream snapshot’s size. You can’t delete a snapshot that has a schedule associated with it.

##### Listing and Describing Snapshots
To list snapshots run the following command: 
```
gcloud compute snapshots list --project PROJECT_ID 
	Flags available 
		--limit maximum number of results you want back 
		--regexp a filter for results you want returned 
		--sort-by field to sort by 
		--uri only print URI’s of the resources returned 
```


To describe snapshots, which returns creation time, size, and source disk, run the following command: 

```
gcloud compute snapshots describe SNAPSHOT_NAME 
	Flags available 
		--format what kind of format you want printed out 
		--project project to be used for command 
		--quiet disables interactive prompts
```


#### Where To Look
https://cloud.google.com/compute/docs/disks/create-snapshots#listing-snapshots
https://cloud.google.com/compute/docs/disks/create-snapshots#viewing-snapshot
https://cloud.google.com/compute/docs/disks/snapshots#incremental-snapshots

#### Content Mapping
- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M3 Virtual Machines and Networks in the Cloud
- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M3 Virtual Machines
- [Essential Google Cloud Infrastructure: Foundation (On-demand)](https://www.cloudskillsboost.google/course_templates/50)
	- M3 Virtual Machines
- [Elastic Google Cloud Infrastructure: Scaling and Automation (On-demand)](https://www.cloudskillsboost.google/course_templates/178)
	- M2 Load Balancing and Autoscaling

### Managing Google Kubernetes Engine Resources

#### Pods
A pod Is the smallest deployable object in Kubernetes. It is a single instance of a running process that contains one or more docker containers. Pods provide networking and storage to containers, and contain dependencies the container needs to run and communicate.

#### Deployment
A deployment manages a set of multiple identical pods. It uses a replica set to define the number of pods. A deployment monitors pods in a replica set and replaces unhealthy instances to ensure your application remains available. A deployment uses a pod template, which provides a spec of what each deployed pod should look like. When you update the pod template in a deployment, it starts a rolling upgrade of the pods in the deployment.

#### Service
A service is a group of pod endpoints that you can configure access for. You use selectors to define which pods are included in a service. A service gives you a stable IP that belongs to the service. Pods have internal IP addresses but they can change as pods get restarted and replaced. A service can be configured to implement load balancing.

#### Load Balancer
To implement network load balancing you create a service object with these settings: 
- type: LoadBalancer. 
- Set External Traffic Policy to cluster or local

##### Cluster
Traffic will be load balanced to any healthy GKE node and then kube-proxy will send it to a node with the pod.

##### Local
Nodes without the pod will be reported as unhealthy. Traffic will only be sent to nodes with the pod. Traffic will be sent directly to pod with source id header info included.

#### Application Load Balancers
To implement an external Application Load Balancer, create an ingress object with the following settings:
- Routing depends on URL path, session affinity, and the balancing mode of backend Network endpoint groups (NEGS) 
- The object type is ingress. 
- Using `ingress.class: “gce”` annotation in the metadata deploys an external load balancer. 
- External load balancer is deployed at Google Points of presence. 
- Static IP for ingress lasts as long as the object.

To implement an internal Application Load Balancer, create an ingress object with the following settings: 
- Routing depends on URL path, session affinity, and balancing mode of the backend NEGS.  
- The object kind is ingress. 
- Metadata requires an `Ingress.class: “gce-internal”` to spawn an internal load balancer. 
- Proxies are deployed in a proxy only subnet in a specific region in your VPC. 
- Only NEGs are supported. Use the following annotation in your service metadata: 
	- `cloud.google.com/neg: '{"ingress": true}'` 
- Forwarding rule is assigned from the GKE node address range.

#### kubectl Commands
You execute kubectl commands to manage objects such as pods, deployments, and services.

Imperative commands such as run, create, replace, delete act on a live object or single config file and overwrite any state changes that have occurred on an existing object.

Declarative commands use a config stored in a directory to deploy and apply changes to your app objects.
- uses `kubectl` -apply on a directory
- You don’t specify create, replace or delete commands.

##### Example Commands

`kubectl -run` 
- Generates a new object in a cluster, by default of deployment
`kubectl -create`
- Generates a new object from a config file
`kubectl -get`
- Displays requested resources
`kubectl -expose`
- Creates a new service that distributes traffic to labelled pods

Pods are not created by themselves but are based on template made available in deployments.

You can use the name of an existing object or defined config file. The object you create service for can be one of the following: deployment, service, replica set, replication controller or pod.

Important specs in a deployment manifest:
- kind: Deployment
- Replicas: 3
- Spec: template specifies labels, container name, and image it is based on

If you need to change a deployment you change the config file and do a `kubectl -apply`

Important specs in a service manifest: 
- Kind: service 
- Spec:selector - labels of pods included in service - have to match them all 
- Port: incoming port 
- targetPort: port the pod is listening on

#### Where To Look
https://cloud.google.com/kubernetes-engine/docs/concepts/kubernetes-engine-overview
https://cloud.google.com/kubernetes-engine/docs/concepts/pod
https://cloud.google.com/kubernetes-engine/docs/concepts/deployment
https://cloud.google.com/kubernetes-engine/docs/concepts/service
https://cloud.google.com/kubernetes-engine/docs/concepts/ingress-ilb
https://cloud.google.com/kubernetes-engine/docs/concepts/ingress-xlb
https://cloud.google.com/kubernetes-engine/docs/how-to/load-balance-ingress
https://cloud.google.com/kubernetes-engine/docs/how-to/internal-load-balance-ingress

#### Content Mapping
- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M5 Containers in the Cloud
- [Getting Started with Google Kubernetes Engine (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/2)
	- M3 Kubernetes Architecture
	- M4 Kubernetes Operations
- Skill Badge
	- [Develop your Google Cloud Network](https://www.cloudskillsboost.google/course_templates/625)


### Managing Cloud Run Resources

#### Autoscaling in Cloud Run

Cloud Run automatically scales the number of container instances required for each deployed revision. When no traffic is received, the deployment automatically scales to zero.

Other ways you can affect Cloud Run autoscaling: 
- CPU utilization, with a default 60% utilization. 
- Concurrency settings, with a default of 80 concurrent requests. You can increase it to 1000. You can also lower it if you need to. 
- Max number of instances limits total number of instances. It can help you control costs and limit connections to a backing service. Defaults to 1000. Quota increase required if you want more. 
- Min number of instances keeps a certain number of instances up. You will incur cost even when no instances are handling requests. 
 
Instances that are started might remain idle for up to 15 minutes to reduce latency associated with cold starts. You don’t get charged for these idle instances. You set a min and max on the container tab in the advanced settings dialog.

#### Where To Look
https://cloud.google.com/run/docs/about-instance-autoscaling

#### Content Mapping

- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M6 Applications in the Cloud


### Managing Storage and Database Solutions

#### Cloud Storage Lifecycle Actions
Lifecycle management configurations apply to current and future objects in a Cloud Storage bucket. When object metadata meets the criteria of any of the rules, Cloud Storage performs a specified action.

##### Examples
- Downgrade the storage class of objects older than 365 days to coldline storage. 
- Delete an object that existed before a certain date. 
- Keep the 3 most recent versions of each object in a bucket with versioning enabled.

Object metadata has to match all rules for the action to fire. If an object state matches more than one rule set, delete takes precedence, followed by storage class with lowest price.

Here are the available conditions: 
- Age 
- Createdbefore 
- Customtimebefore 
- Dayssincecustomtime 
- Dayssincenoncurrent 
- Islive 
- Matchesstorageclass 
- Noncurrenttimebefore 
- numberofnewerversions

#### Where To Look

https://cloud.google.com/storage/docs/lifecycle

#### Content Mapping

- [Google Cloud Fundamentals: Core Infrastructure (ILT and On-demand)](https://www.cloudskillsboost.google/course_templates/60)
	- M4 Storage in the Cloud
- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M5 Storage and Database Services
- [Essential Google Cloud Infrastructure: Core Services (On-demand)](https://www.cloudskillsboost.google/course_templates/49)
	- M2 Storage and Database Services


### Managing Networking Resources

#### Expanding IP Addresses in a Subnet

Command syntax: 

```
gcloud compute networks subnets expand-ip-range SUBNET --prefix-length = PREFIX_LENGTH 
```

If 10.0.128.0/24 you can supply 20 to reduce your mask, which increases your number of available ip addresses.

#### Where To Look

https://cloud.google.com/sdk/gcloud/reference/compute/networks/subnets/expand-ip-range
https://cloud.google.com/vpc/docs/using-vpc#expand-subnet

#### Content Mapping

- [Architecting with Google Compute Engine (ILT)](Architecting with Google Compute Engine (ILT))
	- M2 Virtual Networks

- [Essential Google Cloud Infrastructure: Foundation (On-demand)]
	- M2 Virtual Networks



### Monitoring and Logging

Performance monitoring is another important aspect of managing the day-to-day operations of  cloud solutions and is provided by [[Google Cloud Observability]].

#### Cloud Monitoring
Allows you to build charts based on metrics you specify. You can also look at logs associated with resources from the dashboard. 

#### Custom Metrics
Allow you to define metrics descriptors for things you want to keep track of that aren’t included in standard metrics.

#### Cloud Logging
Allows you to log any timestamped data in logs you define and manage. There are a myriad of options for where you can save your logs and how to route them. There is also an interface provided to query your logs.

#### Cloud Observability
Provides several tools that will help you with performance issues. Error Reporting, Cloud Trace, and Cloud Profiler all help you figure out what might be causing latency and performance issues in your apps.

#### Cloud Operations Custom Alerts
In Cloud Monitoring you implement alerts by defining alert policies. An alerting policy specifies what you want to be alerted on and how you want to be notified. The “what” is made of conditions that describe the state of a resource, or groups of resources, that cause you to take action. The “how” is provided by notification channels, where you specify who is notified when the condition of the alerting policy is met. Each notification channel configures a different type of output, such as email, slack channel, or posting a message to pub/sub topic. You can also specify documentation you want included in your notification.

Conditions are made of a monitored resource, a metric for that resource, and the threshold where the condition is met. An alerting policy can have up to 6 conditions. In an alerting policy with 1 condition, when that condition is met, an incident is created. For an alerting policy, you specify how those conditions are combined.

#### Where To Look
https://cloud.google.com/monitoring/alerts/using-alerting-ui
https://cloud.google.com/monitoring/alerts

#### Content Mapping

- [Architecting with Google Compute Engine (ILT)](https://cloud.google.com/learn/training/class-schedule#/title=Architecting_with_Google_Compute_Engine)
	- M7 Resource Monitoring

- [Essential Google Cloud Infrastructure: Core Services (On-demand)](https://www.cloudskillsboost.google/course_templates/49)
	- M4 Resource Monitoring

- Skill Badges
	- [Set Up an App Dev Environment on Google Cloud](https://www.cloudskillsboost.google/course_templates/637)
	- [Develop your Google Cloud Network](https://www.cloudskillsboost.google/course_templates/625)
