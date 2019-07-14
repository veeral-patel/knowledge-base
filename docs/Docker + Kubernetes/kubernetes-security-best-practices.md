# K8s Security Best Practices (Container Camp 2018)

[Talk on YouTube](https://www.youtube.com/watch?v=v6a37uzFrCw)

## Background

- Guestbook app with Redis cluster, API, web frontend
- Say attacker found a remote code execution vulnerability in frontend

## Attack 1

- Get Kubernetes token from frontend pod, make calls to Kubernetes cluster’s API, extract secrets
- A pod is a group of containers. Every pod has a token that can be used to call the Kubernetes API

### Mitigation

- Add RBAC: Run the frontend pod under a user who can’t read secrets, for example
- Restrict access to API server to specific IP addresses
- Add network policy to block frontend from connecting with Redis instance

## Attack 2

- Attacker can break out of the container to access the host

### Mitigation

- Run as non-root
- Read-only filesystem
- Disallow privilege escalation
- Can sandbox pods (can use `gVisor`, `kata`)
- Restrict Kubelet permissions
