# CH2 - Pods

From [Kubernetes in Action](https://www.manning.com/books/kubernetes-in-action)

## What is a pod?

- A pod groups multiple containers
- All containers of a pod run on the same nod

## Why do we even need pods?

- Each container should run exactly 1 process
- Pods exist so you can pretend multiple processes are running on the same machine
  - In reality, they’re running on the same node (but on different containers)
  - Say RabbitMQ requires 2 processes - create 2 containers in 1 pod

## Each pod has its own port space

- Containers in a pod that bind to the same port will create a port conflict
- A port conflict can’t happen between containers in different pods, though

## The inter-pod network is flat

- Each pod has an IP address
- And any pod can access any other pod at the other pod’s IP address

## Organizing containers across pods

- Organize applications into multiple pods
  - Each pod contains only tightly related components
  - For example - 1 main container plus helper containers
    - `main` = a web server that serves files from a folder
    - `helper` = periodically downloads files into folder
- Run web app and database in different pods, for example
  - Can break web app further into pods -- ie, separate pods for GraphQL and REST APIs
- K8s scales pods, not individual containers
  - If you need to scale a container individually, make it a separate pod
- If in doubt, create a separate pod
