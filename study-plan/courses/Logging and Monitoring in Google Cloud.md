
## I. Why We Need Observability Tools

### Cloud vs On-Premises Challenges

- **On-premises**: Physical access to servers for troubleshooting
- **Cloud**: No physical access to Google's servers
- **Solution**: Use Google's integrated observability tools

### Key Question

_"How do you know what's happening with your server, database, or application in the cloud?"_

---

## II. Four Recurring User Needs for Observability

### 1. Visibility into System Health

- **Purpose**: Understand what's happening with applications and systems
- **Key Questions**:
    - Are my systems functioning?
    - Do my systems have sufficient resources available?
- **Requirements**: Clear mental model and health reports

### 2. Error Reporting and Alerting

- **Features**:
    - Healthy/unhealthy status icons
    - Red/green indicators
    - Proactive alerting and anomaly detection
- **Goal**: Avoid users having to "connect the dots"

### 3. Efficient Troubleshooting

- **Requirements**:
    - Single interface (no multiple tabs)
    - Proactive correlation of relevant signals
    - Easy search across logs and metrics
    - Opinionated recommendations for investigation
    - Immediate action capabilities (e.g., quota increase buttons)

### 4. Performance Improvement

- **Capabilities**:
    - Retrospective analysis
    - Trend analysis for intelligent planning
    - Impact assessment of system changes

---

## III. Monitoring Fundamentals

### Definition

> "Collecting, processing, aggregating, and displaying real-time quantitative data about a system, such as query counts and types, error counts and types, processing times, and server lifetimes."
> 
> _— Google's Site Reliability Engineering book_

### Why Monitoring is Critical

- **Foundation** of product reliability
- **Reveals** urgent attention needs
- **Shows** application usage trends
- **Enables** better capacity planning
- **Improves** client experience

### Key Components for Reliability

- Adequate deployment capacity
- Thorough automated testing
- Refined CI/CD pipeline
- Postmortems and root cause analysis
- Transparency for trust building

### Incident Response Process

1. **Triggering Event**: Outage, data loss, monitoring failure, manual intervention
2. **Response**: Automated systems + DevOps personnel
3. **Signal Examination**: Monitor data analysis
4. **Impact Evaluation**: Escalation when needed
5. **Initial Response**: Formulated action plan
6. **Communication**: Keep customers informed

---

## IV. The Four Golden Signals

### 1. Latency 🕐

**Definition**: Time it takes for a system part to return a result

**Why Important**:

- Directly affects user experience
- Indicates emerging issues
- Tied to capacity demands
- Measures system improvements

**Sample Metrics**:

- Page load latency
- Requests waiting for threads
- Query duration
- Service response time
- Transaction duration
- Time to first response
- Time to complete data return

### 2. Traffic 🚦

**Definition**: Number of requests reaching your system

**Why Important**:

- Indicates current system demand
- Historical trends for capacity planning
- Core measure for infrastructure spend

**Sample Metrics**:

- HTTP requests per second
- Static vs. dynamic content requests
- Concurrent sessions

### 3. Saturation 📊

**Definition**: How close to capacity a service is

**Why Important**:

- Indicates service fullness
- Focuses on constrained resources
- Tied to performance degradation

**Sample Metrics**:

- Memory utilization percentage
- Thread pool utilization percentage
- Cache utilization percentage

### 4. Errors ❌

**Definition**: Events measuring system failures or issues

**Why Important**:

- Indicates configuration/capacity issues
- Shows SLO violations
- Reveals system flaws

**Sample Metrics**:

- Wrong answers/incorrect content
- 400/500 HTTP codes
- Failed requests
- Exceptions

---

## V. [[Google Cloud Observability]]

### Signal Flow

1. **Signal Capture**: Metrics, logs, and traces from hardware layer up
2. **Integration**: Into Google Cloud products
3. **Visualization**: Dashboards and Metrics Explorer
4. **Analysis**: Logs Explorer for automated and custom logs
5. **Monitoring**: SLO compliance and error budget tracking
6. **Health Checks**: Uptime and latency monitoring
7. **Alerting**: Automated alerts to code and personnel

### Key Tools for Operations

#### Core Monitoring Tools

- **[[Cloud Monitoring]]**: System performance and health
- **[[Cloud Logging]]**: Log collection and analysis
- **[[Error Reporting]]**: Crash analysis and counting
- **[[Cloud Trace]]**: Request tracing
- **[[Cloud Profiler]]**: Application performance profiling

#### Additional Capabilities

- Service Level Objectives (SLOs) monitoring
- Error budget tracking
- Health checks for external services
- Automated alerting systems
- Troubleshooting visualization tools


