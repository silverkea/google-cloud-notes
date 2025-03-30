
Virtual machines can be configured like a physical server by specifying the number of CPUs, amount of memory, and the size and type of disk.

Machine properties can be chosen by
- selecting a predefined machine type
- creating a custom machine type

Maximum number of CPUs per VM is determined by "machine family", and constrained by quota available to the user, which is zone dependent.

Can be created via the Google Cloud Console, the `gcloud` command-line tool, or the Google Cloud API.

## Cloud Marketplace

Offers solutions for Google and third party vendors. 

Most software packages in Cloud Marketplace are available at no additional charge, but some may have additional costs.

## Pricing and Billing Structure

Compute Engine bills by the second with a one-minute minimum.

Sustained use discounts are automatically applied to instances that run for more than 25% of the month for each additional minute thereafter.

Committed use discounts are available providing up to 57% discount for committing to usage terms of one or three years.

### Preemptible VMs and Spot VMs

Ideal for batch processing and non time critical workloads - e.g. analyzing large dataset.

Compute Engine has permission to terminate job if resources are needed elsewhere. Therefore jobs need to be able to be stopped and restarted.

Allows saving costs, up to 90% in some cases. 

Preemptible VMs run for maximum 24 hours. 

Spot VMs have more features do not have maximum run time. 

Pricing is same for both.


## Autoscaling and Load Balancing

Allows VMs to be added or removed based on load and metrics.

Requires load balancing to distribute traffic to VMs. [[Virtual Private Cloud]] supports different kinds of load balancing.

Compute Engine does allow for creating large instances, such as for in memory databases.

Most customers prefer to scale out, not up.

## Available Machine Types
cloud.google.com/compute/docs/machine-types

