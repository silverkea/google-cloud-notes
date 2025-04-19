
Kubernetes is an open source container orchestration system for automating computer application deployment, scaling, and management.

Google developed Kubernetes (GKE) originally to support their own internal operations and then made it available as open source technology.

Containers in GKE are based on images which are shared via [[Artifact Registry]]

GKE consists of multiple [[Compute Engine]] instance grouped together to form a cluster.

Can create Kubernetes clusters with Kubernetes Engine by using Google Cloud Console, gcloud command line tool from Cloud SDK, or REST API.

To start a Kubernetes cluster on GKE, run:

```
gcloud container clusters create k1
```

## Modes

### Autopilot Mode
Manages underlying infrastructure including node configuration, autoscaling, auto-upgrades, baseline security configurations, baseline networking configuration.
- Optimized for production
- Strong security posture
- Promotes operation efficiency

### Standard Mode
You manage underlying infrastructure including configuring the individual nodes. Same functionality as Autopilot mode but you are responsible for configuring, managing & optimizing the cluster. Not recommended unless specific level of control is required.

 
## Advanced Cluster Management Features

- Google Cloud's load balancing for [[Compute Engine]]
- Node pools for designating subsets of nodes in a cluster for additional flexibility
- Automatic scaling of cluster's node instances
- Automatic upgrades for clusters node software
- Node auto-repair to repair node health and availability
- Logging and monitoring with [[Google Cloud Observability]]



 
 
