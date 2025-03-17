
- [[Cloud Storage]]
- [[Cloud SQL]]
- [[Cloud Spanner]]
- [[BigQuery]]
- [[Firestore]]
- [[BigTable]]

## Choosing Data Storage

### Unstructured
- [[Cloud Storage]] is best
- Storage class needs to be decided, or let Autoclass choose automatically

### Structured or Semi-Structured

#### Transactional Workloads
Online transaction processing, OLTP - fast data inserts and updates required to build row-based records
##### SQL Access
- [[Cloud SQL]] for local to regional scalability
- [[Cloud Spanner]] for global scalability

##### NoSQL Access
- [[Firestore]] would be best option for transactional NoSQL document-oriented database

#### Analytical Workloads
Online analytical processing, OLAP - where entire datasets need to be read

##### SQL Access
- [[BigQuery]] allows analyzing petabyte scale datasets

##### NoSQL Access
- [[BigTable]] provides scalable NoSQL solution for analytical workloads

