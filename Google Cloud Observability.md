Unified platform for managing and gaining insights into the performance, availability, and health of applications and infrastructure deployed on Google Cloud.

Used to be called Google Cloud Operations Suite and Stackdriver before that.

- Automatically discovers cloud resources and application services based on deep integration with Google Cloud and Amazon Web Services
- Provides access to data and analytics tools and collaboration with third party tools
- Includes services for monitoring, logging, error reporting and tracing
- Billing is usage based with free usage allotments
## Cloud Monitoring
- Comprehensive view of cloud infrastructure and applications
- Collects metrics, logs and traces
- Provides insights into performance, health, availability
- Dynamic config and intelligent defaults
- Monitor platform, system, and application metrics
	- Ingest metrics, events, metadata
	- Generate insights through dashboards, charts, alerting policies
- e.g. Uptime / health checks
- Alerting policy can also be created for when  Cloud Observability is approaching threshold for billing

### Metric Scope
- Root entity that holds monitoring and configuration information in Cloud Monitoring
- Can have from 1 to 375 monitored projects
- Contains dashboards, alerting policies, uptime checks, notification channels, and group definitions for monitored projects
- Accesses metric data from monitored projects, metrics data and logs remain in the individual projects
- First project in the metric scope is the scoping project, specified when creating scope. Name of project becomes name of metric scope.

#### Connecting AWS account
- Requires configuring a project in Google Cloud to hold AWS Connector

#### Access Control
- "Single pane of glass" for viewing all resources from multiple projects / AWS accounts
- All users have access to all data by default
	- Role assigned ton one person on one project applies equally to all projects in the metric scope
- To give people different roles per-project, consider placing monitoring of projects in different metric scopes

### Alerting Best Practices
- Alert on symptoms, not the cause - e.g. failing queries of a database
- Use multiple notification channels - email, SMS
- Customize alerts to audiences needs by describing what actions are needed or what to examine
- Avoid noise so alerts are not dismissed / ignored over time
- Adjust alerts so they are actionable, not just alerting everything possible

### Uptime Checks
- Test availability of public services from locations around the world
- Supports HTTP, HTTPS, TCP
- Can check [[App Engine]] apps, [[Compute Engine]] instances, URL of a host, or AWS instance or load balancer
- Can create alerts and view latency of each global location

### Ops Agent
- Because VMs on Compute Engine run on Google hardware, hypervisor can't collect some internal metrics - e.g. memory usage
- Ops Agent collects metrics inside the VM, not at hypervisor level
- Primary agent for collecting telemetry data from Compute Engine instances
- Collected metrics can be used in dashboards, alerts, uptime checks and notifications
- Can configure Ops Agent to monitor many [third-party applications](https://cloud.google.com/monitoring/agent/ops-agent/third-party)

### Custom Metrics

- Can create custom metrics from applications
- Can use these in dashboards, alerts, and notifications, and trigger auto scaling

### Autoscaling
- To maintain a metric at target value, specify a utilization target
- Autoscaler will add or remove instances to maintain the target
- If metric comes from each instance, autoscaler will average the metric across all instances
- If metric applies to instance group, autoscaler will use the metric from the group
- For metrics with multiple values, apply a filter to select the value to use

## Cloud Logging
- Allows you to store, search, analyze, monitor and alert on log data and events from Google Cloud and AWS
- Fully managed service, performs at scale
- Collects and stores application and infrastructure logs
- Provides ability to troubleshoot issues, identify trends, comply with regulations
- Includes storage for logs, Logs Explorer interface, and API for managing logs programmatically
- Retention is 30 days, can be exported to 
	- Cloud Storage, 
	- Pub/Sub, 
	- BigQuery - can the use logging data with Looker Studio

## Error Reporting
- Counts, analyzes and aggregates the errors in your running cloud services
- Centralized error management interface displays results, with sorting, filtering and notification capabilities via email, mobile app, pub/sub, webhooks
- Dedicated view shows details
	- Time chart
	- Occurrences
	- Affected user count
	- First and last seen
	- Cleaned exception traces
- Available for App Engine (standard and flexible), Apps Script, Compute Engine, Cloud Functions, Cloud Run, Google Kubernetes Engine and Amazon EC2
- Stack trace parser available for Go, Java, Node.js, Python, Ruby, PHP, .NET

## Cloud Trace
- Collect latency data from applications and display in Cloud console
- Track how requests propagate through your application and receive detailed near real-time performance insights
- Helps identify performance bottlenecks in applications
- Generate in-depth latency reports that surface performance degradation
- Can capture traces from App Engine, Google Cloud client libraries, Google Kubernetes Engine (GKE), Cloud Run services, Cloud Functions, HTTPS(S) load balancers and applications instrumented with Cloud Trace API
- Language specific client libraries: Java, Go, Node.js, Python, Ruby, PHP, .NET
- Supports OpenTelemetry, Zipkin, OpenCensus

## Cloud Profiler
- Continuously analyzes CPU power, memory and other resources and application uses
- Uses statistical techniques (sampling) and low-impact instrumentation to provide picture of application performance without slowing it down.
- Allows developers to analyze applications running anywhere, including on-premises, in Google Cloud, or other clouds.
- Supported languages: Java, Go, Node.js, Python


## Partner Integrations

![[cloud-observability-partner-integrations.png]]


### Logging and Monitoring Reference Architecture

#### BindPlane Ingestion

![[cloud-observability-bindplane-import.png]]

#### Splunk Enterprise Export

![[cloud-observability-splunk-enterprise-export.png]]


