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

