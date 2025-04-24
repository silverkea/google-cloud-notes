Flexible horizontally scalable NoSql cloud database for storing and syncing data in real-time.

Directly accessible by mobile and web applications.

Storage in form of collections of documents.

Provides automatic scaling with no loss of performance

Also provides for offline data access.

Querying:

- Retrieve individual documents
- Retrieve all documents in a collection
- Can include multiple chained filters
- Can combine filtering and sorting options
- Indexed by default - query performance is proportional to size of result set, not size of data set

Supports data synchronization to update data on any connected device

Actively used data is cached, so the app can write, read, listen to, and query data even if the device is offline.

When the device comes back online, Firestore synchronizes local changes back to Firestore

Google Cloud's infrastructure provides

- automatic multi-region data replication
- strong consistency guarantees
- atomic batch operations
- real transaction support

Key Features:
- Simplifies storing, syncing and querying data
- Fast, fully managed serverless cloud native NoSQL document database 
- Suitable for Mobile, web and IoT apps at global scale
- Client libraries provide live synchronization and offline support
- Security features
- Accelerate building serverless apps
- ACID transaction support
- Automatic multi-region replication and strong consistency
- Powerful query engine - run sophisticated queries without performance degradation

Datastore mode:
- Next generation of Cloud Datastore 
- can operate in Datastore mode for backward compatibility
- strong consistency - queries no longer eventually consistent
- no longer limited to 25 entity groups per transaction, writes to entity group no longer limited to 1 per second

Native mode:
- Strongly consistent storage layer
- Collection and document data model
- Real-time updates
- Mobile and Web client libraries

To access all Cloud Firestore features, use the Native mode.

General Guide: Use Datastore mode only for new server projects, and native mode for mobile and web apps.

![[firestore-or-bigtable-decision-tree.png]]