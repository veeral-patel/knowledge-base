# Docker Security (GOTO 2016)

[Talk on YouTube](https://www.youtube.com/watch?v=A32Yjizt2_s)

## Guidelines

- Don’t run containers as root
- Disable capabilities (like SETUID, SETGID) with `—-cap-drop`
- Limit Docker containers’ memory usage
- Use minimal images
- Use SELinux or AppArmor
- Verify images with Docker Content Trust
- Only use official or popular images
- Immutable containers
- Audit images with `docker diff`
- Scan for vulnerabilities (`schlock`, `twistlock`, `clair`)
- Set `read-only` flag to stop Docker container from writing to host's filesystem

## Ways to store secrets

- Environment variables
- Run Vault (as a Docker container)

## Use VMs to separate groups of containers

- For multi-tenancy - each customer’s containers in a separate VM
- For different security levels - different VM for credit card processing, for example

## An Attacker Looks at Docker (BlackHat 2018)

[Talk on YouTube](https://www.youtube.com/watch?v=HTM3ZrSvp6c)

- Speaker gets code execution on a Joomla web server
- He runs an nmap scan to enumerate the backend containers - `postgres`, `node.js`, `redis`
- Inserts votes into the Postgres DB and Redis instance (they don’t have authentication enabled)
