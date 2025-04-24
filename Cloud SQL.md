Fully managed relational databases for structured data.

Relational database types
- MySql
- PostreSQL
- SQL Server


Google Responsible For:
- Applying patches / updates
- Managing backups
- Configuring replications

Can scale up to 128 processor cores, 864 GB RAM, and 64 TB of storage, 60000 IOPS.

Greater than 99.95% availability

Data Migration Service (DMS) makes it easy to migrate production databases to Cloud SQL with minimal downtime.

Support for replication from
- Cloud SQL primary instances
- External primary instances
- External MySQL instances

Managed backups
- Backed up data stored securely
- Cost of instance covers seven backups

Encryption
- Data encrypted while stored in tables, temporary files and backups, and while on internal networks

Network Firewall
- Control access to each database instance

Accessibility
- Accessible from other Google Cloud services and external applications -e.g. Cloud Shell, App Engine, Google Workspace scripts
- Use with App Engine using standard drivers - Connector/J for Java and MySQLdb for Python
- Compute Engine instances can be configured to access Cloud SQL instances, and can be in same zone as  your VM
- Support for other applications and tools like SQL Workbench, Toad and other applications using standard drivers

High Availability Configuration
- Synchronous replication to each zone's persistent disk
- All writes made to primary instance are replicated to disks in both zones before transaction reported as committed
- Automatic failover to standby instance in case of failure

Scaling
- Scale up - requires a machine restart
- Scale out - using read replicas

Connecting

![[cloud-sql-connection-options.png]]

- Private IP connection 
	- most performant and secure 
	- connect application in same project and region as Cloud SQL instance
	- traffic never exposed to public internet
- Cloud SQL Auth Proxy
	- for connecting from another region / project, or outside Google Cloud
	- handles authentication, encryption, key rotation
- Manual SSL configuration
	- for control over the SSL connection
- Unencrypted connection
	- connection from a specific IP address via an external IP address

