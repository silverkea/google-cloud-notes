- Serverless managed compute platform running stateless containers via web requests or Pub/Sub events.
- Built on Knative - open API and runtime build on Kubernetes.
- Fully managed on Google Cloud, [[Google Kubernetes Engine|GKE]] or anywhere Knative runs.
- Auto scale almost instantly from zero to N instances.
- Usage charged to nearest 100 milliseconds, plus start up and shut down time, plus small fee per million requests.
- Price of container time increases with CPU and memory.
- Can run any binary compiled for Linux 64 bit.
- Supports languages including Java, Python, Node.js, PHP, Go, Ruby, .NET, and C++.
- Can also run code written in less popular languages, e.g. Cobol, Haskell, Perl
- If application handles web requests, good to go.

Cloud Run provides unique HTTPS URL for deployed container images, starts container on demand, ensures it is running, and scales it up or down as needed.
## Development Workflow

### Container Based

1. Write application in favourite programming language - should start web server that listens for web requests.
2. Build an package application into a container image.
3. Push container to [[Artifact Registry]] where Cloud Run will deploy it.

### Source Based

Cloud Run will deploy the source code directly without needing to build a container image. 

Achieved using [Buildpacks](https://cloud.google.com/docs/buildpacks/overview) - an open source project that transforms application source code into a container image.




