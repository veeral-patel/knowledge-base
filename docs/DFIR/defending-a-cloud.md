# Defending a cloud

[Talk on YouTube](https://www.youtube.com/watch?v=F_yvc5QlKvI)

## What is a cloud?

A collection of automated datacenters that's:

- Deployed by machines
- Managed by machines
- Monitored by machines

Humans plug in the hardware and the software takes it from there

### Primary resources of a cloud

- Compute
- Storage
- Network (eg, ZScaler)

## How a cloud is architected

- Lots of redundancy!
- 1 compute node can have a few TB of RAM

A compute node has:

- Network/disk
- Host OS
- Hypervisor
- A bunch of guest VMs

### Big picture

A cloud has:

- physical infra
- nodes running VMs
- services (eg, hosted Hadoop)
- tenant VMs (equivalent of EC2 instances)

## Attack surface of a cloud

- Attacking physical infra -- requires breaking into datacenter
- Attacking nodes -- requires escaping the guest VMs somehow
- Attacking services -- difficult to do because Microsoft keeps them patched
- Tenant VMs -- want to attack this layer, because companies may neglect to patch and/or secure these VMs

## Shared security model

- Microsoft doesn't want to take responsibility for how you use your VM
- Microsoft is responsible for the cloud infrastructure and you are responsible for your application

## Painful parts of defending a cloud

### The cloud changes quickly, making forensics hard

- Attacker can shut down and erase a disk quickly
- IP addresses change all the time
- In Azure, the customer owns their VM--Microsoft can't gather forensic artifacts from a customer's VM without
  the customer's consent or a warrant

### Clouds are of massive scale

- Azure is orders of magnitude larger than enterprise networks
- Standard DFIR doesn't scale to the cloud

## Pleasant parts of defending a cloud

### Collecting forensic evidence is easy

- A VM's disk is just a file on a physical disk--and so are memory dumps
- Can take snapshots of VMs
- You can take the virtual disk, put it into a different VM, and boot it!

### You can leverage the cloud

You have:

- Unlimited compute
- Unlimited storage
- Unlimited bandwidth

- For each infected VM, you can spin up a VM to analyze its memory dump
- And you can do this for thousands of VMs, at once, quickly
- To summarize: you can obtain and process large amounts of evidence quickly and in parallel

### Remediation is easy

- If you have an autoscaling fleet running an app, and 1 host is infected, you can just re-deploy the fleet
- This can be done in 1 command with docker-compose up, kubectl restart, etc

### Easy to know what the baseline is

- All the VMs in a fleet should have the same applications, accounts, processes, registry entries etc
- If one VM differs from the other VMs, then it may be compromised
- We can build a baseline and then alert on hosts that deviate from it
- Even better, we could build a baseline of accepted behaviors, whitelist those behaviors, and reject all other behaviors
