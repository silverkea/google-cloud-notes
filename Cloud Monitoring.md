## What is Cloud Monitoring?

Cloud Monitoring is Google Cloud's service that provides visibility into the **performance, uptime, and overall health** of cloud-powered applications.

## Data Collection

**Sources:**

- Projects, logs, services, systems
- Agents and custom code
- Common application components (Cassandra, Nginx, Apache Web Server, Elasticsearch, etc.)

**Data Types:**

- Metrics
- Events
- Metadata

## Output & Insights

Cloud Monitoring processes collected data and generates insights through:

- **Dashboards**
- **Metrics Explorer charts**
- **Automated alerts**

## Key Advanced Capabilities

### 1. **Cost-Effective Monitoring**

- **1,500+ free metrics** across 100+ monitored resources
- No cost for basic monitoring capabilities

### 2. **Open Source Standards**

- **Prometheus** integration
- **OpenTelemetry** support
- Works across compute workloads

### 3. **Workload-Specific Customization**

- **GKE**: Custom visualization via Google Cloud Managed Service for Prometheus
- **Compute Engine**: Custom visualization through Ops Agent

### 4. **Integrated Experience**

- **In-context visualizations and alerts**
- View telemetry data alongside workloads across Google Cloud
- Seamless integration with Google Cloud services


# Common Monitoring Architecture Patterns

## Typical Cloud Monitoring Architecture

Cloud Monitoring includes **3 main layers**:

### Data Collection Layer

- Collects **metrics, logs, and traces** from cloud-based systems
- In Cloud Monitoring, includes Google Cloud services:
    - Google Kubernetes Engine
    - Compute Engine
    - App Engine

### Data Storage Layer

- **Stores collected data**
- **Routes to configured visualization** and analysis layer
- In Cloud Monitoring: **Cloud Monitoring API**
    - Helps triage collected metrics
    - Stores data for further analysis

### Data Analysis and Visualization Layer

- **Analyzes collected data** to identify problems and trends
- **Presents data** in easy-to-understand format
- In Cloud Monitoring includes:
    - **Dashboards** for data visualization
    - **Uptime checks** for application monitoring
    - **Alerting policies** for notifications and events

## Platform Monitoring

### Blackbox Monitoring

- **Most common use** of Cloud Monitoring
- Provides **visibility into Google Cloud services performance**
- **Enabled by default** with automatic system metrics collection
- **No user effort required**

### System Metrics Benefits

- **Available at no cost** to customers
- Provide information about **service operations**
- **Over 1,500 metrics** across **100+ Google Cloud services** automatically
- **Example**: Compute Engine reports **25+ unique metrics** per VM instance

### Third-Party Integration

- Customers can use **Cloud Monitoring APIs** to ingest metrics into partner products
- Enables aggregation with **traditional enterprise monitoring tools**

## Application Monitoring Solutions

### GKE Workloads - Google Managed Prometheus (GMP)

**For GKE applications**, customers prefer **Prometheus-based solutions**:

#### GMP Features

- **Part of Cloud Monitoring**
- Makes **GKE cluster and workload metrics** available as Prometheus data
- **Ingests monitoring data** in Prometheus format
- Supports **PromQL compatible query language**
- **Natively integrated**:
    - Prometheus expression browser
    - Prometheus compatible rule evaluation

**Recommendation**: Use **Google Managed Prometheus for GKE workloads**

### Compute Engine Workloads - Ops Agent

**For Compute Engine applications**, use **Ops Agent** to:

- Collect **in-process metrics**
- Collect metrics from **third-party applications** running in VMs

#### Ops Agent Capabilities

- Supports **30+ plugins** for different open source and ISV software
- Collects **richer, fine-grained metrics** at OS level
- **Windows and Linux support** (multiple flavors)
- **Based on OpenTelemetry standards**

#### Custom Application Support

- Custom applications can use **OTEL client libraries** for code instrumentation
- Ops Agent can **collect custom metrics** and make them available in Cloud Monitoring

## Partner Solutions

### When to Consider Partners

- If **ecosystem of third-party plugins** doesn't meet needs
- Consider partner products like:
    - **Datadog**
    - **NewRelic**

### Partner Integration Benefits

- **API-based integrations** with Google Cloud platform
- Can collect **system metrics** from Google Cloud

## Hybrid Cloud Monitoring - BindPlane

### BindPlane by Blue Medora

Imports monitoring and logging data from:

- **On-premises VMs**
- **Other cloud providers**:
    - Amazon Web Services (AWS)
    - Microsoft Azure
    - Alibaba Cloud
    - IBM Cloud

### Single Pane of Glass Architecture

#### Advantages

- **Deep integration** for **150+ popular data sources**
- **No additional licensing costs** for using BindPlane
- Comprehensive hybrid cloud visibility

#### Pricing Structure

- **BindPlane metrics**: Imported as **custom metrics** (chargeable)
- **BindPlane logs**: Charged at **same rate** as other Cloud Logging logs

### Result

Cloud Monitoring and BindPlane provide **unified monitoring** across hybrid cloud environments.

# Metrics Scope

## What is Metrics Scope?

### Default Behavior

- When you create a Google Cloud project, it **automatically hosts a metrics scope**
- Becomes the **scoping project** for that scope
- **Stores**: alerts, uptime checks, dashboards, monitoring groups
- **Each project creates its own metrics scope** by default

### Key Rules

- **One metrics scope** can monitor **multiple projects**
- **One project** can only be monitored by **a single metrics scope**
- Must decide which relationship works best for your organization

---

## Option 1: Local Project Monitoring

### Setup

Every project monitored **locally within that project**

### ✅ **Advantages**

- **Clear separation** for each project
- **Easy access control** - dev personnel can access development resources
- **Co-location** - project resources and monitoring in same place
- **Easy automation** - monitoring becomes standard part of project setup

### ❌ **Disadvantages**

- **Limited visibility** for applications spanning multiple projects
- No unified view across related projects

---

## Option 2: Centralized Metrics Scope

### Setup

**Single metrics scope** monitors **multiple projects**

### How It Works

- Add multiple projects to existing scope
- Monitoring data for **all projects visible** in one place
- Create **cross-project dashboards**
- Set **alerting policies** across multiple projects

### 🏆 **Recommended Approach for Production**

Create **dedicated monitoring project** to:

- Host monitoring configuration data
- Use its metrics scope to monitor actual resource projects
- **Prevent monitoring loss** if resource projects get deleted

### ✅ **Advantages**

- **Single pane of glass** for entire group of related projects
- **Easy comparison** between non-prod and prod environments
- Unified monitoring across application stack

### ❌ **Disadvantages**

- **Broad access permissions** - anyone with Cloud Monitoring IAM can see all environments
- **No team separation** - doesn't preserve production team divisions
- **Monitoring Viewer role** applies to ALL projects in scope by default

---

## Important IAM Considerations

### Access Control Reality

- Metric data and logs **remain in individual projects**
- **Monitoring Viewer role** grants access to:
    - All dashboards
    - All data across the metrics scope
- Role assigned to one person **applies equally** to all monitored projects

### Security Implication

Choose metrics scope strategy carefully based on your **access control requirements**

---

## Scope Limitations

### What Metrics Scope Affects

- **Only Google Cloud resources** related to **Cloud Monitoring**

### What It Doesn't Affect

The following tools are **strictly project-based** and **don't use metrics scope**:

- **Cloud Logging**
- **Error Reporting**
- **Application Performance Management (APM) tools**

These tools don't rely on:

- Metrics scope configuration
- Monitoring IAM roles

---

## Key Decision Framework

### Choose **Local Project Monitoring** When:

- Need strict project separation
- Small, independent applications
- Team access needs vary by project

### Choose **Centralized Metrics Scope** When:

- Application spans multiple projects
- Need unified monitoring view
- Teams share monitoring responsibilities
- Want to compare environments easily

**Remember**: This decision primarily affects Cloud Monitoring - other observability tools remain project-scoped regardless.