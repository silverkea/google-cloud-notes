
## Data Centers
- Designed to deliver exceptional reliability, security and efficiency
- Committed to minimizing environmental impact
- Zero-trust architecture ensuring security at every level
- Tamper-evident hardware, secure boot , hardware based encryption
- Physical security with robust access control and biometric authentication
- Least privilege principle implemented
- Embody security by default
- Resilience as a core principle, equipped to withstand and recover from security incidents
- Efficiency delivered via purpose built servers optimized for specific tasks
- Scalability delivered by quickly being able to accommodate new hardware

## Secure Storage
- Automatically encrypt all customer content at rest without any effort required from customer
- Self management of keys available via [[Cloud Key Management Service]] (Cloud KMS)
- Robust security to ensure authenticity, integrity and privacy of data in transit
- Data encrypted and authenticated at multiple network layers, especially when travelling outside Google controlled physical boundaries
- Data in use encrypted via memory encryption making it nearly impossible for unauthorized users to gain access
- Advanced Encryption Standard (AES) in use for encryption

## Identity
- Three A's principle - Authentication, Authorization, Auditing
- Authentication - validation of credentials, preferably two step verification (2ST) / two-factor authentication / multi-factor authentication.
- Authorization - determine what the user or system is allowed to do
- Auditing - tracking user activities within the system
- [[Identity and Access Management (IAM)]] - centralized and efficient approach to managing access control within Google Cloud environment

## Network Security
- Zero trust security implemented via Google Cloud's BeyondCorp Enterprise Security model.
- User's identity and context considered in every access request
- Private access methods available via [[Cloud VPN]] and [[Cloud Interconnect and Peering]] allowing secure connections between on-premises networks and cloud resources
- Perimeter secured via firewalls and [[Virtual Private Cloud|Virtual Private Cloud (VPC)]]
- Utilize [[Shared Virtual Private Cloud|Shared VPC]] to separate each Google Cloud Project so they work independently and safely
- Prevent DDoS attacks with web application firewall (WAF) via [[Google Cloud Armour]]
- Automate provisioning and create immutable infrastructure using tools like [[Terraform]], [[Jenkins]] and [[Cloud Build]] to create secure and reliable cloud environments

## Security Operations (SecOps)
- [[Security Command Center|Security Command Center (SCC)]] provides centralized view of security posture
- [[Cloud Logging]] to collect and analyze security logs from entire cloud environment
- Expert incident responders available across various domains with knowledge and tools to tackle security incidents



