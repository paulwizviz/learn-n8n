# Our Deployment Adventures

As we delve deeper into n8n, we've started to explore the different ways we can get our workflows running in a more permanent setup. It's one thing to run n8n on our local machines, but another entirely to have a stable, scalable environment that we can rely on.

In these notes, we'll be documenting our findings on a couple of popular methods for deploying n8n using containers:

1. **Docker Compose:** This seems to be the most straightforward path. We've found it's perfect for getting a single-node instance up and running quickly, which is great for smaller projects or development environments where you just want to get going without much fuss.

2. **Kubernetes (K8s):** For a more robust, scalable, and resilient setup, we're looking into Kubernetes. It's definitely more complex, but the payoff should be a production-grade deployment that can handle heavier loads and provide high availability. We'll share what we learn as we go.

We hope our notes are helpful as you embark on your own n8n deployment journey.

## Docker

For our Docker-based setup, we're using a combination of a `docker-compose.yaml` file and a helpful `ops.sh` script to make managing it a bit easier. Here’s a quick rundown of what to expect.

* **[Deployment Specification](../deployments/docker/docker-compose.yaml)**: This file defines our n8n environment. We're using the official `n8nio/n8n` image and have set it up to persist all our workflow data into a local `n8n-data` directory. This is crucial so we don't lose our work when the container restarts. It also sources a number of environment variables from the `ops.sh` script to configure things like the host, port, and basic authentication.

* **[Operational Scripts](../deployments/docker/ops.sh)**: This is a simple shell script we've put together to handle the common operations. It allows us to `start` and `stop` the n8n container. There's also a `clean` command, but a word of caution: **it will permanently delete all your n8n data**, so use it with care! It's really only there for when we need a completely fresh start.

We've noticed a small issue in the `ops.sh` script where the path to the `docker-compose.yaml` file seems to be incorrect. It points to a `single` directory, but it should be pointing to the `docker` directory. We'll need to get that fixed to get the script working correctly.

## Kubernetes

While our Docker Compose setup is great for getting started, we're now thinking about what a more production-ready Kubernetes deployment would look like. This is where things get a bit more involved, but the benefits in scalability and resilience are well worth the effort. Here's the approach we're planning to take:

* **StatefulSet for the Core:** Instead of a simple Deployment, we think a `StatefulSet` is the right choice for the n8n pods. This will give us stable network identifiers and, most importantly, stable persistent storage, which is a must for keeping our workflow data safe.

* **Persistent Storage:** We'll use a `PersistentVolumeClaim` (PVC) to request storage from the cluster. This PVC will then be bound to a `PersistentVolume` (PV), ensuring that our n8n data directory (`/home/node/.n8n`) survives pod restarts and failures.

* **Configuration with ConfigMaps and Secrets:** We want to separate our configuration from the container image. We'll use a `ConfigMap` to store non-sensitive settings. For all our secrets—like database credentials, API keys, and the basic auth username and password—we'll be using Kubernetes `Secrets`. This is a much more secure way to handle sensitive data.

* **Exposing n8n with a Service and Ingress:** To make n8n accessible, we'll first create a `Service` (likely of type `ClusterIP`) to provide a stable internal endpoint for the n8n pods. Then, we'll set up an `Ingress` resource. The Ingress will manage external access to our n8n instance, handle TLS for HTTPS, and route traffic from our chosen hostname to the n8n service.

This is our initial blueprint. It's definitely more complex than the Docker Compose version, but we're confident it will give us a robust and scalable foundation for running n8n in a more demanding environment. We'll be sharing our YAML files and findings here as we build it out.

> NOTE
>
> A working deployment is still under construction.