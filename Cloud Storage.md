Durable and highly available object storage. 99.999999999% durability.

Objects stored in a package format
- Binary form of data
- Metadata - e.g. creation date, author, resource type, permissions
- Globally unique identifier - in the form of URL

No minimum fee, pay only for what you use.

Provisioning extra capacity is not required.

Data is encrypted on the server side before writing to disk.

Transport is secured using HTTPS/TLS (Transport Layer Security)

## Key Features
- Scalable to exabytes
- Time to first byte in milliseconds
- Very high availability across all storage classes
- Single API across all storage classes
- Support for customer supplied encryption keys (CSEK)
	- use own key instead of Google managed keys
- Directory synchronization
	- synchronize a VM directory with a bucket
- Object change notifications using Pub/Sub
- Strong global consistency - successful operations on objects immediately available from any location where Google offers service - includes:
	- Read after write
	- Read after metadata update
	- Read after delete - download object or metadata gets 404 afterwards
	- Bucket listing
	- Object Listing

## Storage Classes
- Standard 
	- best for frequently accessed data, or data stored only briefly
- Nearline Storage 
	- best for infrequently accessed data - read/write once a month or less
	- 30 day minimum storage duration
- Coldline Storage 
	- meant for reading / modifying at most once every 90 days
	- 90 day minimum storage duration
- Archive Storage 
	- best for data accessed less than once a year. 
	- Minimum 365 storage duration.

![[storage-class-decision-tree.png]]

### Common Characteristics
- Unlimited storage
- Worldwide accessibility and locations
- Low latency and high durability
- Uniform Experience
- Geo-Redundancy if stored in a multi-region or dual-region

### Autoclass
Moves data that is not accessed to colder storage category, and moves data that is accessed to standard storage to optimize future access. 
- All objects added to bucket in Standard class regardless of request options
- No charges for early deletion, retrieval or storage class transitions


## Location Types
Google Cloud Storage offers three types of locations for storing your data:

### 1. Region

- Data stored in a specific geographic location (e.g., us-central1, europe-west4)
- Lowest latency within that region
- Lower cost than multi-region
- Good for region-specific workloads and data residency requirements

### 2. Dual-region

- Data replicated across two specific regions
- Designed for high availability while maintaining geographic control
- Good for analytic workloads that need data in specific locations
- Higher availability than single region

### 3. Multi-region

- Data stored redundantly across multiple regions in a larger geographic area
- Predefined areas like "US", "EU", or "ASIA"
- Highest availability and protection against regional outages
- Typically higher cost than regional storage
- Best for frequently accessed content distributed globally

## Buckets

Cloud Storage files are organized into buckets.

- Buckets have a globally unique name and are located in specific regions. Location should be chosen to minimize latency for majority of users.
- Location type can't be changed from regional to multi-regional / dual-region or vice versa.
- e.g. if most users are in Europe, choose a location in Europe, or the EU multi-region.
- Can create directories but really a directory is another object that points to different objects in the bucket.

## Objects
- Objects are the actual files stored in Cloud Storage.
- Inherit storage class of bucket when created unless specified on the object.
- Storage class can be changed without moving object to different bucket.
- No minimum size for objects, unlimited storage


## Versioning
- Storage objects are immutable. A new version of an object is created when the object is modified.
- Administrators have the option to either allow each new version to overwrite the old version, or to track changes by enabling versioning within a bucket.
- If versioning is not enabled, default behaviour is to overwrite older versions.
- If versioning is enabled, archived versions can be listed, restored, or permanently deleted.
- Versioning can be turn on and off at any time.
- Turning versioning off leaves existing versions in place and causes bucket to stop accumulating new versions.

## Soft Delete
- Bucket level protection against accidental / malicious deletion or modification of objects.
- Preserves all recently deleted objects for specified time.
- Enabled by default with retention duration of 7 days.

## Controlling Access

- Access control is managed through [[Identity and Access Management (IAM)|IAM]] roles, and where needed access control lists (ACLs). 
- Roles are inherited from project to bucket to object. Sufficient for most purposes.
- ACLs can be created for finer control. Limit of 100 ACL entries per bucket. 
	- ACLs contain two pieces of information: 
		- the scope (user or group) being granted access, and 
		- the actions being granted - such as read, write. 
	- Examples:
		- `collaborator@gmail.com` - a specific user
		- `allUsers` - anyone on the internet
		- `allAuthenticatedUsers` - anyone authenticated with Google account
- Signed URL provide a cryptographic that gives time limited access to a bucket or object.
- Signed policy document determines what kind of file can be uploaded by someone with a signed URL


## Object Lifecycle Management

- Lifecycle management allows you to automatically delete objects after a specified period of time, or to transition objects to a different storage class, or limit number of versions retained.
- Can be relative or absolute time periods.
- Can also determine how many versions are kept in buckets with versioning enabled.
- Rules applied in asynchronous batches, so may not be immediate.
- Changes to lifecycle rules may take up to 24 hours to take effect.


## Object Retention Lock
- Define retention requirements on per object basis
- Governs how long object must be retained
- Options to prevent retention time from being reduced or removed


## Transferring Data

- Data can be transferred to and from Cloud Storage using the glcoud storage command line tool, the API, or the Google Cloud Console (with drag and drop in Google Chrome).
- Storage Transfer Service 
	- enables importing large amounts of data into Cloud Storage quicky and cost effectively
	- can be used to schedule transfers from http(s) endpoints, other Cloud Storage regions or other cloud storage providers to Cloud Storage.
- Transfer Appliance
	- rackable high-capacity storage server that you can use to transfer large amounts of data to Google Cloud.
	- connect it to network, load it with data, ship it to upload facility where data is upload to Cloud Storage.
	- can transfer up to a petabyte of data on single appliance
- Offline Media Import
	- Third party provider uploads data from physical media
- Integration with other Google Cloud products, for example:
	- import / export tables to and from [[BigQuery]] and [[Cloud SQL]]
	- store [[App Engine]] logs, [[Cloud Firestore]] backups, and objects used by [[App Engine]] applications like images
	- store instance startup scripts, [[Compute Engine]] images, and objects used in [[Compute Engine]] applications
