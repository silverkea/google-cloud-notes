
- Collection of identical VM instances controlled as single entity using template
- Update by specifying new template in rolling update
- Scale automatically to number of instances in the group when required
- Work with load balancing services to distribute traffic to instances
- Automatic recreation with same name and template of instance if unhealthy / stop / crash / delete by actions other than instance group commands
- Regional MIG preferred over Zonal to 
	- allow spread of application load across zones 
	- avoids managing multiple MIGs across different zones
	- protect against zonal failures and entire group of instances in a zone malfunctioning


## Creation
- Create a template - similar to creating an instance, but choices are recorded
- Create a MIG of N instances
	- Type - stateless (web server, batch processing)  / stateful (database, legacy app)
	- Name
	- Single / Multi zonal, and choose locations
	- Optionally provide port mapping details
	- Template to use
	- Autoscaling configuration
	- Health check configuration
- Instance group manager automatically populates group based on template

## Autoscaling
- Policies include scaling by
	- CPU utilization
	- Load balancing capacity
	- Monitoring metrics
	- Queue based workload like Pub/Sub
	- Schedule - start time, duration, recurrence

## Health check
- Define protocol, port and health criteria
- GCP computes health state for each instance
- Health criteria defines 
	- check interval - frequency of checks
	- timeout - how long to wait
	- healthy threshold - how many success result is decisive
	- unhealthy threshold - how many failed result is decisive

## Stateful IP address
- Ensure applications continue to function during auto-healing, update and recreation
- Internal & external IPv4 addresses can be preserved
- Allows automatic or manual assignment of IP to VM instances in a MIG

