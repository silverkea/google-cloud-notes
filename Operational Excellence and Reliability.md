

## Fundamentals of Cloud Reliability

### Four Golden Signals for Site Reliability

#### Latency 
- How long to return a result
- Directly affects user experience
- Changes indicate emerging issues
- Used to measure system improvements

#### Traffic
- How many requests reach your system
- Trends used for capacity planning
- Core measure when calculating infrastructure spend

#### Saturation
- How close to capacity a system is
- Focuses on the most constrained resources
- Tied to degrading performance

#### Errors
- Raised when a flaw, failure or fault occurs
- Indicate failure, configuration or capacity issues, service level objective violations, or need for alerts

### Site Reliability Targets

#### Service-Level Indicators (SLIs)
- Measures of how well system is performing, such as response time, error rate, uptime percentage
#### Service-Level Objectives (SLOs)
- Goals set for performance based on SLIs

#### Service-Level Agreements (SLAs)
- Agreements between a cloud service provider and its customer
- Promises and guarantees regarding quality of service
- Includes agreed upon SLOs, performance metrics, uptime guarantees and any penalties or remedies for failure to meet commitments
- Penalties or remedies may include refunds or credits when an outage is longer than the agreement allows


## Designing Resilient Infrastructure and Processes


### High Availability
Ability of a system to remain operational and accessible even if hardware or software failures occur

### Disaster Recovery
Process of restoring a system to functional state after a major disruption or disaster


### Key Design Considerations

#### Redundancy
- Duplicating critical components or resources to provide backup alternatives
#### Replication
- Creating multiple copies of data or services and distributing them across different locations
#### Regions
- Data center locations where resources can be distributed to for improved resilience
- Multiple regions should be utilized to mitigate against unavailability of any particular region
#### Scalable Infrastructure
- Dynamic allocation and deallocation of resources based on workload fluctuations
- Autoscaling adjusts resource capacity to match demand
#### Backups
- Regular backups of data and configuration to guard against data loss, hardware failures, cyber attacks
- Cloud providers offer backup services that can be automated with secure storage and easy restoration
- Backups should be stored in geographically separate locations to protect against regional outages or disasters

### Regular Testing, Validation and Monitoring
Recovery processes should be regularly tested and validated to ensure correct function during real-world incidents.

Monitoring, alerting and incident response mechanisms should be implemented to identify and address issues promptly.


## Observability Tools

Tools for collecting, analyzing and visualizing data to gain insights into performance, health and behaviour.

### [[Google Cloud Observability]]
Comprehensive set of monitoring, logging and diagnostics tools

## Google Customer Care

### Basic Support
- Free and included for all customers
- Access to documentation, community support, Cloud Billing Support and Active Assist recommendations

### Standard Support
- Recommended for workloads under development
- Unlimited access to tech support for troubleshooting, testing and exploration
- Individual access to English speaking support reps during work hours 5 days a week
- Access to Cloud Support API for integrating Cloud Customer Care with your organizations CRM

### Enhanced Support
- Recommended for workloads in production
- Support available 24/7 in a selection of languages and faster initial response times
- Technical support escalations and third party technology support

### Premium Support
- Recommended for enterprises with critical workloads
- Fastest response time and dedicated Technical Account Manager
- Customer Aware Support where Customer Care learns and maintains information about architecture, partners and Google Cloud projects
- Credit for Google Cloud Skills Boost training program
- Event management service for planned peak events like product launches, major sales, etc
- Operational health reviews to measure progress and address blockers to achieving goals

### Value-Add Services
- Available for Enhanced and Premium support plans

## Support Case Lifecycle
Support cases can be created on Google Cloud console by Standard, Enhanced and Premium plan customers.

- Case creation 
	- can be done by users with Tech Support Editor role
	- important to select priority from P4 to P1
- Case triage
- Case assignment
- Troubleshooting and investigation
- Communication and updates
- Escalation - appropriate when there is a break in process or communication issue
- Resolution and mitigation
- Validation and testing
- Case closed