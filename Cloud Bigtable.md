Google's NoSQL big data database service

Powers services like Search, Analytics, Maps, Gmail

Designed to 
- handle large workloads
- provide consistent low latency and high throughput


Key Features:
- Petabyte-scale
- Consistent sub-10ms latency
- Seamless scalability for throughput
- Learns and adjusts to access patterns
- Ideal for Ad-Tech, Fintech, and IoT
- Storage engine for ML applications
- Easy integration with big data tools like Hadoop, [[Cloud Dataflow]], [[Cloud Dataproc]]
- Supports open source industry standard HBase API




![[cloud-bigtable-decision-tree.png]]

Good solution for:
- Operational and analytical applications - IoT, user analytics, financial analytics
- More than 1 TB of semi-structured data that is rapidly changing or requiring high throughput
- Read/write latency of less than 10 milliseconds together with strong consistency
- NoSQL data
- Data that is time-series or has natural ordering
- Working with big data, running asynchronous batch or synchronous real-time processing
- Running machine learning algorithms on data

Smallest Cloud Bigtable cluster is 3 nodes handling 30000 operations per second. Usage charges apply while operational, regardless of whether application is using them or now.

Consider [[Cloud Firestore]] as alternative for smaller applications.

Integration with other Google Cloud services and third party clients
- APIs provided to read/write data through a data service layer like Managed VMs, HBase REST Server, or a Java Server using the HBase client - typically used to serve data to applications, dashboards, data services
- Data can be streamed through stream processing frameworks like Dataflow Streaming, Spark Streaming and Storm
- Batch processing frameworks like [[Cloud Dataflow]], Spark, and Hadoop
- Summarized or newly calculated data is often written back to Bigtable or to a downstream database



## Cloud Bigtable Storage

![[cloud-big-table-storage.png]]

- Massively scalable tables, each of which is key/value map
- Comprised of rows, each describing single entity, and columns containing values for each row
- Row indexed by single row key
- Related columns typically grouped into column families
- Row/column intersection can contain multiple cells or versions at different timestamps, providing record of how data was altered over time
- Tables are sparse - cells without data do not occupy space
- New column qualifiers can be added as data changes

![[cloud-bigtable-processing.png]]
- Processing is handled separately from storage
- Table is sharded into blocks of contiguous rows called tablets for balancing workload of queries
	- Similar to HBase regions from HBase API
- Tablets stored on Colossus - Google's file system, in SSTable format
	- Provides persistent, ordered, immutable map from keys to values where keys and values are arbitrary byte arrays
- If a Bigtable node is frequently accessing a subset of data, Bigtable will update indexes so other nodes can distribute workload evenly
- Throughput scales linearly up to hundreds of nodes


