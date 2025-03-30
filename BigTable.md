Google's NoSQL big data database service

Powers services like Search, Analytics, Maps, Gmail

Designed to 
- handle large workloads
- provide consistent low latency and high throughput

Good solution for:
- Operational and analytical applications - IoT, user analytics, financial analytics
- More than 1 TB of semi-structured data that is rapidly changing or requiring high throughput
- NoSQL data
- Data that is time-series or has natural ordering
- Working with big data, running asynchronous batch or synchronous real-time processing
- Running machine learning algorithms on data

Integration with other Google Cloud services and third party clients
- APIs provided to read/write data through a data service layer like Managed VMs, HBase REST Server, or a Java Server using the HBase client - typically used to serve data to applications, dashboards, data services
- Data can be streamed through stream processing frameworks like Dataflow Streaming, Spark Streaming and Storm
- Batch processing frameworks like Dataflow, Spark, and Hadoop
- Summarized or newly calculated data is often written back to Bigtable or to a downstream database

