Durable and highly available object storage

Objects stored in a package format
- Binary form of data
- Metadata - e.g. creation date, author, resource type, permissions
- Globally unique identifier - in the form of URL

No minimum fee, pay only for what you use.

Provisioning extra capacity is not required.

Data is encrypted on the server side before writing to disk.

Transport is secured using HTTPS/TLS (Transport Layer Security)

## Storage Classes
- Standard - best for frequently accessed data, or data stored only briefly
- Nearline Storage - best for infrequently accessed data - read/write once a month or less
- Coldline Storage - meant for reading / modifying at most once every 90 days
- Archive Storage - best for data accessed less than once a year. Minimum 365 storage duration.

### Common Characteristics
- Unlimited storage
- Worldwide accessibility and locations
- Low latency and high durability
- Uniform Experience
- Geo-Redundancy if stored in a multi-region or dual-region

### Autoclass
Moves data that is not accessed to colder storage category, and moves data that is accessed to standard storage to optimize future access.


## Buckets

Cloud Storage files are organized into buckets.

- Buckets have a globally unique name and are located in specific regions. Location should be chosen to minimize latency for majority of users.
- e.g. if most users are in Europe, choose a location in Europe, or the EU multi-region.

## Versioning
- Storage objects are immutable. A new version of an object is created when the object is modified.
- Administrators have the option to either allow each new version to overwrite the old version, or to track changes by enabling versioning within a bucket.
- If versioning is not enabled, default behaviour is to overwrite older versions.
- If versioning is enabled, archived versions can be listed, restored, or permanently deleted.


## Controlling Access

- Access control is managed through [[Identity and Access Management (IAM)|IAM]] roles, and where needed access control lists (ACLs). 
- Roles are inherited from project to bucket to object. Sufficient for most purposes.
- ACLs can be created for finer control. ACLs contain two pieces of information: 
	- the scope (user or group) being granted access, and 
	- the actions being granted - such as read, write. 

## Lifecycle Management

- Lifecycle management allows you to automatically delete objects after a specified period of time, or to transition objects to a different storage class.
- Can be relative or absolute time periods.
- Can also determine how many versions are kept in buckets with versioning enabled.


## Transferring Data

- Data can be transferred to and from Cloud Storage using the glcoud storage command line tool, the API, or the Google Cloud Console (with drag and drop in Google Chrome).
- Storage Transfer Service 
	- enables importing large amounts of data into Cloud Storage quicky and cost effectively
	- can be used to schedule transfers from http(s) endpoints, other Cloud Storage regions or other cloud storage providers to Cloud Storage.
- Transfer Appliance
	- rackable high-capacity storage server that you can use to transfer large amounts of data to Google Cloud.
	- connect it to network, load it with data, ship it to upload facility where data is upload to Cloud Storage.
	- can transfer up to a petabyte of data on single appliance
- Integration with other Google Cloud products, for example:
	- import / export tables to and from [[BigQuery]] and [[Cloud SQL]]
	- store [[App Engine]] logs, [[Firestore]] backups, and objects used by [[App Engine]] applications like images
	- store instance startup scripts, [[Compute Engine]] images, and objects used in [[Compute Engine]] applications
