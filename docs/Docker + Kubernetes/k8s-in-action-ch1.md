# CH1 - Introducing Kubernetes

From [Kubernetes in Action](https://www.manning.com/books/kubernetes-in-action)

## Control Plane

Runs on Kubernetes master node (or nodes, for HA)

### Components

- API Server
- Scheduler - schedules your pods
- Controller Manager - Performs cluster-level functions, like replicating components, tracking worker nodes, handling node failures, etc
- Etcd - Distributed data store

## Nodes

Machines that run your containerized applications

### Components

- Container runtime - Docker, rkt, etc
- Kubelet - talks to API server and manages containers on its node
- Kubernetes Service Proxy (kube-proxy) - load balances network traffic between application components

## Running an application in Kubernetes

1. Create container images for your application
2. Push images to an image registry
3. Send a description of your app to the Kubernetes API server

## Pods

- A pod is a group of containers. You can have different (but usually closely related) containers in a pod
- A pod’s containers are always run on the same host
- You can replicate a pod on multiple nodes, if you need more of a container
