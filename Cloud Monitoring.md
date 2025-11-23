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

# Cloud Monitoring Data Model and Visualization

## Time Series Data Structure

### Core Concept

Monitoring data is recorded in **time series**, each containing **four key pieces of information**:

### 1. Metric Field

- **Metric-label**: One combination of label values
- **Metric type**: Specifies available labels and describes what data points represent

### 2. Resource Field

- **Resource-label**: One combination of label values
- **Monitored resource**: Specific source where data was collected

### 3. MetricKind and ValueType Fields

- **Value type**: Data type for measurements
- **Metric kind**: How to interpret values relative to each other

#### Three Types of Metrics:

- **Gauge metric**
- **Delta metric**
- **Cumulative metric**

### 4. Points Field

- **Array of timestamped values**
- Metric type defines what values represent

---

## Example Time Series Structure

### Sample Components

- **Metric**: `logging.googleapis.com/log_entry_count` with severity level INFO
- **Resource**: Compute Engine instance with specific instance and project ID
- **Metric kind**: DELTA type
- **Value type**: Integer
- **Points**: Array of timestamp and metric value

---

## Dashboard Creation Workflow

### Step-by-Step Process

1. **Identify** Google Cloud Monitoring resources to monitor
2. **Check** Monitoring Dashboards for auto-created dashboards
3. **Use Metrics Explorer** when auto-dashboards insufficient
4. **Monitor** 1,500+ metrics and build custom dashboards

### Dashboard Benefits

- **Graphical representations** of signal data
- **Decision-making support** for Google Cloud resources
- **Auto-created dashboards** for common resources (VMs, GKE clusters)
- **Opinionated default information** from Google

---

## Metrics Explorer Features

### Core Capabilities

- **Build charts** for any metric collected by project
- **Save charts** to custom dashboard
- **Share charts** by URL
- **View configuration** as JSON
- **Explore data** without long-term display needs

### Interface Components

1. **Configuration region**: Pick metric and options
2. **Chart display**: Shows selected metric
3. **Display panel**: Configure axis, threshold lines, etc.

---

## Chart Configuration Elements

### Metric Selection

Must specify:

- **Monitored resource type**
- **Metric type** (metric descriptor)

### Filtering

- **Reduces data** returned for metric
- **Excludes time series** not meeting criteria
- **Filter options**:
    - Resource group
    - Name
    - Resource label
    - Metric label
- **Operators**: Direct values or regular expressions

### Grouping

- **Combines different time series**
- Specify **grouping** and **function**
- **Grouping by**: Label values
- **Function**: How time-series data combines into new series

### Alignment

- **Regularizes raw data** in time
- **Creates regularly spaced data**
- **Required** before combining time series
- **Automatic** with default values, customizable

#### Alignment Components:

- **Alignment period**: Time subdivision length (default: 1 minute)
- **Alignment function**: How to summarize data (sum, mean, etc.)

---

## Chart Display Options

### Analysis Modes

1. **Standard mode**: Each time series with unique color
2. **Stats mode**: Common statistical measures display
3. **X-Ray mode**: Translucent gray lines, useful for many lines

### Additional Features

#### Compare to Past

- **Modified legend** with two "values" columns
- **Today** vs **past period** (e.g., Last Week)

#### Threshold Line

- **Horizontal reference line** from Y-axis point
- **Visual reference** for threshold values
- **Left or right Y-axis** options

#### Legend Alias

- **Customizable descriptions** for time series
- **Template support** with variables
- **Plain text and expressions** supported
- **Evaluated** when legend displays

### Configuration Tips

- **Click column headers** to sort legend
- **Widget type** and **analysis mode** determine display
- **Legend columns** are configurable
- **Templates** provide better descriptions than default labels

---

# Query Languages for Cloud Monitoring

## Overview

Two advanced query languages provide more versatile interaction with metrics beyond the standard Metrics Explorer interface:

- **Monitoring Query Language (MQL)**
- **PromQL**

---

## Monitoring Query Language (MQL)

### What is MQL?

- **Advanced query language** for Cloud Monitoring
- **Expressive, text-based interface** to time-series data
- Enables **retrieve, filter, and manipulate** time-series data

### Key Use Cases

- **Create ratio-based charts and alerts**
- **Perform time-shift analysis** (week over week, month over month, year over year)
- **Apply mathematical, logical, table operations** and other functions to metrics
- **Fetch, join, and aggregate** over multiple metrics
- **Select arbitrary percentile values** (not just predefined ones)
- **Create new labels** to aggregate data using string manipulations and regular expressions
- **Unlimited advanced use cases** for joins, arbitrary percentages, and complex calculations

### How MQL Works

- **Built using operations and functions**
- **Pipe idiom**: Output of one operation becomes input to the next
- **Incremental building** of complex queries
- **Similar to Linux command line** chaining and piping

---

## PromQL Integration

### What is PromQL?

- **Alternative interface** to Metrics Explorer and MQL
- **Query and chart** Cloud Monitoring data

### Supported Data Sources

- **Google Cloud services** (GKE, Compute Engine) with Cloud Monitoring system metrics
- **User-defined metrics** (log-based metrics, Cloud Monitoring user-defined metrics)
- **Google Cloud Managed Service for Prometheus** (fully managed multi-cloud solution)

### Additional Tools

- **Grafana integration** for charting metric data
- **Available metrics** include Managed Service for Prometheus and documented Cloud Monitoring metrics

---

## Practical Example: Error Rate Analysis

### Scenario

Distributed web service on **Compute Engine VMs** with **Cloud Load Balancing** **Goal**: Analyze error rate (SRE "golden signal")

### Requirement

Chart displaying **ratio of HTTP 500 responses to total requests** (request-failure ratio)

### MQL Query Structure

**Metric**: `loadbalancing.googleapis.com/https/request_count` **Label**: `response_code_class` (captures response code classes)

#### Query Logic - Aggregation Expression:

1. **First sum**: Uses `if` function to count 500-valued HTTP responses (0 for other codes)
2. **Second sum**: Adds counts for all requests using `val()`
3. **Division**: Creates ratio of 500 responses to all responses

**Result**: Request-failure ratio showing error rate over time

---

## How to Access Query Languages

### In Metrics Explorer

1. Navigate to **Metrics Explorer**
2. Click the **CODE** button
3. Use **radio button** to switch between:
    - **MQL**
    - **PromQL**

### Key Benefits

- **More precise control** over data manipulation
- **Advanced analytical capabilities** beyond GUI
- **Flexible querying** for complex monitoring scenarios
- **Integration** with existing Prometheus workflows

---

## When to Use Query Languages

### Choose MQL When:

- Need **advanced mathematical operations**
- Require **complex data joins**
- Want **custom percentile calculations**
- Need **time-shift comparisons**
- Creating **ratio-based monitoring**

### Choose PromQL When:

- Using **Prometheus-based workflows**
- Working with **Managed Service for Prometheus**
- Need **Grafana integration**
- Familiar with **Prometheus query syntax**

## Key Takeaway

Query languages provide **powerful, programmatic access** to Cloud Monitoring data, enabling complex analysis and custom visualizations beyond standard dashboard capabilities.

---

# Uptime Checks

## What are Uptime Checks?

Uptime checks **test the availability** of public services from **locations around the world**.

---

## Configuration Options

### Check Types

- **HTTP**
- **HTTPS**
- **TCP**

### Supported Resources

- **App Engine** applications
- **Compute Engine** instances
- **URL of a host**
- **AWS instances** or load balancers

---

## Key Features

### Monitoring Capabilities

- **Create alerting policies** for each uptime check
- **View latency** from each global location
- **Ensure external services** are running properly
- **Prevent unnecessary error budget burn**

### Check Configuration

- **Frequency**: Checks run every minute
- **Timeout**: 10-second default timeout
- **Failure criteria**: No response within timeout period = failure
- **Success metrics**: Displays uptime percentage and outage tracking

---

## Creation Process

### Basic Setup

1. Navigate to **Monitoring > Uptime Checks**
2. Click **Create Uptime Check**
3. **Name/title**: Descriptive identifier
4. **Select check type protocol**
5. **Choose resource type**
6. **Enter resource information** (e.g., hostname, page path for URLs)

### Advanced Options

- **Logging failures**: Enable failure logging
- **Location filtering**: Narrow global test locations
- **Custom headers**: Add authentication or custom headers
- **Check timeout**: Modify default timeout settings
- **Authentication**: Configure authentication methods

### Alerting Integration

- **Easy alert creation** for failing uptime checks
- **Integrated alerting policies** with Cloud Monitoring

---

## Benefits

- **Global perspective** on service availability
- **Proactive monitoring** of external services
- **Error budget protection** through early detection
- **Comprehensive latency insights** from multiple locations
- **Simple setup** with advanced customization options

## Key Takeaway

Uptime checks provide **essential external monitoring** capabilities to ensure public services remain available from a global perspective, helping maintain service reliability and protect error budgets.

---


## Understanding SLI, SLO, and SLA

### Service Level Indicators (SLIs)

**Definition**: Carefully selected monitoring metrics that measure **one aspect of a service's reliability**

#### Key Characteristics:

- **Close linear relationship** with users' experience of reliability
- **Recommended format**: Ratio of two numbers
    - Number of good events ÷ Count of all valid events
- **Must be quantifiable** and measurable

### Service Level Objectives (SLOs)

**Definition**: Combines a **service level indicator with a target reliability**

#### Typical Targets:

- Generally **just short of 100%** (e.g., 99.9% or "three nines")
- Based on SLI ratios with specific percentage goals

#### S.M.A.R.T. SLO Criteria:

**Specific**:

- ❌ "Is the site fast enough?" (subjective)
- ✅ "95th percentile results returned in under 100ms" (specific)

**Measurable**:

- Must be **numbers or deltas** that can be placed in mathematical equations
- Based on monitoring data grouped over time with math applied

**Achievable**:

- **"100% Availability"** sounds good but is **impossible to obtain/maintain**
- Must be realistic and sustainable

**Relevant**:

- **Does it matter to the user?**
- **Will it help achieve application-related goals?**
- If not, it's a poor metric

**Time-bound**:

- **Specify time period**: per year, month, day?
- **Define calculation method**: specific windows (Sunday to Sunday) or rolling periods (last 7 days)?
- Without time bounds, **accurate measurement is impossible**

### Service Level Agreements (SLAs)

**Definition**: **Commitments made to customers** about system/application uptime limits

#### Key Components:

- **Minimum service levels** promised to customers
- **Consequences** when promises are broken
- **Compensation methods** (refunds, credits) for paying customers during outages
- **Legal/contractual obligations**

#### SLA Limitations:

- **Incentivizes minimum service** levels to prevent customer churn
- **Customers feel impact** before SLA breaches occur
- **Compensation can be expensive** if triggered frequently
- **Reactive rather than proactive** approach

### Relationship Between SLI, SLO, and SLA

#### Example:

- **SLA**: Maintain error rate of **less than 0.3%** for billing system
- **SLI**: Error rate (quantifiable measure)
- **SLO**: 0.3% (specific target)

#### Strategic Implementation:

- **Alerting thresholds** often **substantially higher** than SLA minimums
- Provides **breathing room** to detect problems and take action
- Prevents reputation damage before SLA breach

### Requirements for Effectiveness

#### Business Alignment:

- **All parts of business** must agree SLIs/SLOs accurately measure user experience
- Must **use as primary driver** for decision making
- **Being out of SLO** must have **concrete, well-documented consequences**

#### Operational Consequences:

- **Slow down rate of change**
- **Direct more engineering effort** toward eliminating risks
- **Improve reliability** to meet SLOs faster
- **Strong executive support** needed to enforce consequences and effect change

### Key Takeaway

SLIs, SLOs, and SLAs work together to create a **comprehensive reliability framework** that balances customer expectations, internal targets, and business operations, but require **organization-wide commitment** to be effective.


---

## Alerting Strategy

### What are Alerts?

**Definition**: Automated notifications sent by Google Cloud through notification channels to external applications, ticketing systems, or people

#### When Alerts Are Generated:

- **Service is down**
- **SLO isn't being met**
- **Something needs to change**

### Alert Processing Through Time Series

- **Events processed** through series of data points
- **Broken into successive, equally spaced time windows**
- **Configurable**: Window duration and math applied to data points
- **Enables**: Event summarization, error rate calculation, alert triggering

### Error Budget Alerting

#### Error Budget Formula:

**Error Budget = Perfection - SLO**

#### Example:

- **SLO**: "90% of requests must return in 200ms"
- **Error Budget**: 100% - 90% = **10%**
- **Alert trigger**: When system trending to spend all error budget before allocated time window

### Alerting Strategy Measurement Attributes

#### Precision:

- **Definition**: Proportion of detected alerts that were relevant
- **Formula**: Relevant alerts detected ÷ (Relevant + Irrelevant alerts)
- **Decreased by**: False alerts
- **Represents**: Measure of **exactness**

#### Recall:

- **Definition**: Proportion of relevant alerts that were detected
- **Formula**: Relevant alerts detected ÷ (Relevant alerts + Missed alerts)
- **Decreased by**: Missing alerts
- **Represents**: Measure of **completeness**

#### Detection Time:

- **Definition**: How long system takes to notice alert condition
- **Trade-off**: Long detection times affect error budget; too fast generates false positives

#### Reset Time:

- **Definition**: How long alerts fire after issue resolution
- **Problem**: Continued alerts on repaired systems cause confusion

### Window Length Decision Making

#### Two Types of Windows:

1. **SLO measurement window** (e.g., 99.9% availability over 30-day period)
2. **Alert triggering window** (e.g., alert if errors exceed 0.1% over 60-minute period)

#### Window Length Trade-offs:

**Small Windows**:

- ✅ **Faster alert detection**
- ✅ **Shorter reset times**
- ❌ **Decreased precision** (more false positives)
- **Example**: 10-minute window alerts in 0.6 seconds, consumes 0.02% error budget

**Longer Windows**:

- ✅ **Better precision** (longer confirmation time)
- ❌ **Longer detection and reset times**
- ❌ **More error budget consumed** before alert
- **Example**: 36-hour window alerts in 2min 10sec, consumes 5% error budget

#### Successive Failure Count Strategy:

- **Use short windows** + **require multiple failures**
- **Example**: Three consecutive window failures trigger alert
- **Benefit**: Quick detection but treats single failures as anomalies
- **Downside**: **Inverse precision-recall relationship** - avoiding false positives may miss real issues

### Advanced Alerting Strategies

#### Multiple Conditions Approach:

**Solution**: Define **multiple conditions** in alerting policy to achieve:

- Better precision
- Better recall
- Improved detection time
- Better reset time

#### Multiple Alert Channels:

- **Short window** condition → **Pub/Sub message** → **Cloud Run container**
- **Complex logic** checks multiple conditions before human notification
- **Graduated response** based on severity

### Alert Prioritization and Severity

#### Prioritization Criteria:

- **Customer impact**
- **SLA compliance**
- **Don't involve humans** unless meeting criticality threshold

#### Severity Levels:

- **Custom severity levels** on alert policies
- **Included in notifications** for effective alerting
- **Third-party integration** support
- **Helps focus** on most critical operations issues

#### Notification Channel Strategy:

**High-Priority Alerts**:

- **Slack**
- **SMS**
- **PagerDuty**
- **Multiple channels for redundancy**

**Low-Priority Alerts**:

- **Email**
- **Logging**
- **Support ticket management system**

### Enhanced Notification Channels:

- **Email, Webhooks, PubSub, PagerDuty** accept severity data
- **Enables automation and customization** based on importance
- **Flexible routing** based on alert criticality

### Key Takeaway:

Effective alerting strategy requires **balancing precision and recall** through **multiple conditions, appropriate window sizing, and tiered notification channels** that prioritize based on **customer impact and business criticality**.


---
# Creating Alerts in Google Cloud 

### Alerting Policy Components

An alerting policy consists of:

- **Name** (use descriptive organizational naming conventions)
- **One or more alert conditions**
- **Notifications**
- **Documentation**

### Creation Methods

- **Google Cloud Console** (GUI)
- **gcloud CLI**
- **API**
- **Terraform**

#### File Format Support:

- **JSON or YAML** format for policy definitions
- **Learning tip**: Create alert via console, then use `gcloud monitoring policies list` and `describe` commands to see corresponding definition file

---

## Types of Alerting Policies

### Metric-Based Alerting

- **Purpose**: Track metric data collected by Cloud Monitoring
- **Example**: Notify when application on VM has high latency for significant time period
- **Creation**: Google Cloud console

### Log-Based Alerting

- **Purpose**: Notify when specific message occurs in log
- **Example**: Alert when human user accesses security key of service account
- **Creation**: Logs Explorer in Cloud Logging or Cloud Monitoring API

---

## Alert Conditions Configuration

### Core Components:

- **Target resource and metric** to monitor
- **Filter, group by, aggregate** to exact requirements
- **Trigger logic**: condition, threshold, duration

### Three Types of Metric-Based Conditions:

#### Metric-Threshold Conditions:

- Trigger when metric values **more than or less than threshold** for specific duration

#### Metric-Absence Conditions:

- Trigger when **absence of measurements** for duration window

#### Forecast Conditions:

- **Predict future behavior** using previous data
- Trigger when prediction shows time series will **violate threshold within forecast window**

---

## Notification Options

### Direct-to-Human Channels:

- **Email**
- **SMS**
- **Slack**
- **Mobile Push**

### Third-Party Integration:

- **Webhook**
- **Pub/Sub**

### User-Defined Labels:

- **Add severity indicators** to notifications
- **Enable prioritization** for investigation
- **Parse JSON payload** for third-party routing (PagerDuty, Webhooks, Pub/Sub)

---

## Notification Channel Details

### Channel Characteristics:

- **Email**: Easy and informative, but can become spam
- **SMS**: Fast notifications, choose recipient carefully
- **Slack**: Popular in support circles
- **Google Cloud mobile app**: Valid mobile option
- **PagerDuty**: Third-party on-call management and incident response
- **Webhooks/Pub/Sub**: Alert external systems or code

---

## Documentation Section

### Purpose:

Provide **additional helpful information** to alert recipients

### Best Practices:

- Include **internal playbooks**
- Add **landing links**
- Use **dynamic labels**
- Reference **standard solutions** for common alerts
- **If solution is standard, consider automation instead**

---

## Incident Management

### Incident States:

#### Incidents Firing:

- **Incident is open**
- Alerting policy conditions **being met**
- **No data** indicating condition no longer met
- Usually indicate **new or unhandled alert**

#### Acknowledged Incidents:

- **Technician marks as acknowledged**
- **Signal to others** someone is handling the issue
- Prevents duplicate investigation efforts

#### Closed Incidents:

- Issue resolved and incident closed

### Management Features:

#### Snooze Functionality:

- **Temporarily prevent alerts** from being created
- **Prevent notifications** from being sent
- **Stop repeated notifications** for open incidents
- **Use case**: Escalating outage to reduce new notifications

---

## Groups for Resource Management

### Purpose:

Alert on **behavior of resource sets** instead of individual resources

### Capabilities:

- **Subgroups** up to **six levels deep**
- **Multiple group membership** for resources
- **Physical or logical topology** management
- **Separate production from test/development**
- **Monitor by zone** or other criteria

### Membership Criteria:

- Resource name or type
- Cloud Projects
- Network tag
- Resource label
- Security group
- Region
- App Engine app or service

---

## Logs-Based Metrics

### Definition:

Metrics **extracted from Cloud Monitoring** based on **log entry content**

### Capabilities:

- **Count log entries** containing particular messages
- **Extract latency information** from log entries
- **Use in Cloud Monitoring charts** and alerting policies
- **Serve as basis** for alerting conditions

---

## Terraform Alert Policy Creation

### Required Arguments:

#### Display_name:

- **Identifies policy** with dashboard-visible name

#### Combiner:

- **Defines how results** of multiple conditions combine

#### Conditions:

- **List of conditions** combined based on combiner
- **Maximum**: Six conditions per policy

### Basic Structure:

```
resource "google_monitoring_alert_policy" "alert_policy" { 
	display_name = "Descriptive Alert Name" 
	combiner = "OR" # or "AND" 
	conditions { 
		# condition definition 
	} 
}
```

### Key Takeaway:

Google Cloud alerting provides **flexible, multi-channel notification systems** with **sophisticated condition logic** and **comprehensive incident management** to ensure critical issues receive appropriate attention while minimizing alert fatigue.

---

# Service Monitoring

## Purpose and Scope

### Modern Application Challenges

- **Multiple interconnected services** - when one fails, many appear to fail simultaneously
- **Complex dependencies** require sophisticated monitoring approaches
- **Service Monitoring helps manage this complexity** through SLO and alert creation

### Key Questions Service Monitoring Answers

1. **What are your services?**
2. **What functionality** do services expose to internal/external customers?
3. **What are your promises** regarding availability and performance - **are services meeting them?**
4. **What are inter-service dependencies** in microservices apps?
5. **How to use dependency knowledge** for code rollouts and problem triage?
6. **Can you view all monitoring signals holistically** to reduce MTTR (Mean Time to Repair)?

---

## Supported Service Types

Cloud Monitoring can identify **candidate services** for:

- **GKE namespaces**
- **GKE services**
- **GKE workloads**
- **Cloud Run services**

---

## Service Monitoring Interface

### Services Overview Page

**Entry point** providing:

- **Service name, type, SLO status**
- **SLO-related alert status**
- **Health summary** of various services
- **Filtering capabilities** with Filter text box
- **Click service name** to view detailed monitoring

---

## SLO Compliance Calculation Methods

### Request-Based SLOs

- **Uses ratio**: Good requests ÷ Total requests
- **Example**: Latency below 100ms for ≥95% of requests
- **Success scenario**: 98% of requests faster than 100ms

### Window-Based SLOs

- **Uses ratio**: Good windows ÷ Total windows
- **Each window = single data point** (not all data points within window)
- **Example**: 95th percentile latency <100ms for ≥99% of 10-minute windows
- **Success scenario**: 99% of 10-minute windows were compliant

---

## Request-Based vs Window-Based Comparison

### Example Scenario:

- **1,000,000 requests/month**
- **30-day rolling compliance period**

#### Request-Based (99.9% SLO):

- **1,000 total bad requests** allowed per 30 days

#### Window-Based (99.9% SLO with 1-minute windows):

- **43 bad windows** allowed
- **Calculation**: 43,200 total windows × 99.9% = 43,157 good windows

### Window-Based SLO Limitation:

- **Can hide burst-related failures**
- **Example**: System returns only errors Friday 9:00-9:05 AM
    - Never violates SLO
    - But creates poor user experience during specific time periods

---

## SLO Creation Process

### Step 1: Service Selection

- **Services overview page** → Select listed service
- **Automatic listing** for supported Google Cloud compute technologies

### Step 2: Create SLO Configuration

#### SLI Metric Options:

- **Availability**: Successful responses ÷ All responses
- **Latency**: Calls below threshold ÷ All calls
- **Other**: Custom SLI using Metrics Explorer

#### SLO Type Selection:

- **Request-based** or **Window-based** SLOs

### Step 3: Compliance Period

- **Period Type**: Calendar-based or Rolling
- **Period Length**: Configure duration

### Step 4: Performance Goal

- **Goal percentage** sets performance target for SLI
- **Used to calculate error budget** for SLO

### Step 5: Alerting (Optional)

- **Click "Create alerting policy"** for automatic alert setup

---

## Service Details and Monitoring

### Service Detail View

**Click individual service** to see:

- **Existing SLOs** and expandable details
- **SLI status**
- **Error budget remaining**
- **Current SLO compliance level**
- **Alert status** (if configured)

### SLO Violation Alerting

#### Alert Trigger Logic:

- **Lookback window** examines trends
- **Burn rate threshold** determines alert raising

#### Example Configuration:

- **60-minute lookbook window**
- **7-day SLO period**
- **Burn rate threshold of 1** = 100% error budget usage by end of period
- **Alert trigger**: Trend shows burning through error budget in **1/10th the time** (faster than sustainable)

---

## Monitoring Views

### Available Tabs:

1. **Service Level Indicator**: Current SLI values
2. **Error Budget**: Budget consumption details
3. **Alerts Firing**: Active alert information

### Key Benefit

**Easy post-creation monitoring** of SLI status, error budget, compliance, and alert status in unified interface.

---

## Key Takeaway

Service Monitoring provides **comprehensive SLO management** through automated service discovery, flexible SLO calculation methods, simplified creation workflows, and integrated alerting - enabling **proactive service reliability management** in complex, interconnected service architectures.

---
