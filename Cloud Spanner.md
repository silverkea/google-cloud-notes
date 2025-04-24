Fully managed, mission critical relation database service that scales horizontally to handle unexpected spikes.

Combines benefits of relational database with non-relational horizontal scale

Battle tested by Google's own mission critical applications.

Capabilities:
- Scale to petabytes
- Strong consistency
- High availability
- Used for financial and inventory applications
- Monthly uptime
	- Multi-regional: 99.999%
	- Regional: 99.99%

![[cloud-spanner-capabilities.png]]

Suited for
- SQL relation database with joins and secondary indexes
- Built-in high availability
- Strong global consistency
- High numbers of input/output operations per second


Handles replicas, sharding, acid transaction processing to allow quickly scaling to meet any sage pattern.

## Replication

- Data replicated in end cloud zones, in one region or multi-region
- Database placement is configurable, can choose regions to put database in
- Allows for high availability and global placement
- Replication synchronized across zones using Google's fibre network
- Atomic clocks ensure atomic consistency when updating data


![[cloud-spanner-decision-tree.png]]