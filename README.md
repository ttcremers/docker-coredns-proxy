# Docker CoreDns based nameserver Proxy

When developing using Docker/Docker Compose we usually map ports to the host machine `0.0.0.0:80->80/tcp`, which maps http to our host so we can test a web application, for example.

While this works this isn't always the best solution especially when working on bigger projects with multiple (micro-)services.

Wouldn't it be much nicer if we could find our services under their respective container names under the top level domain `.docker`, that's exactly what this project does. It runs a containerized DNS server mapped to the host on port 53. All DNS queries for `*.docker` are proxied to the internal Docker name server and the containers service ip is returned if a service with that specific `constainer_name` is found.

As the name server runs containerised it works crossplatform (famous last words...)


## Getting started
1. If you don't have the development/docker Docker network create it: `docker network create docker`
2. Start this project `docker compose up -d`
3. Add 127.0.0.1 to your workstations DNS config as primary entry
4. **Done** you should now be able to resolve all hosts in the external docker network
5. Test: `ping ws-dev-proxy-coredns-1.docker`

The service is configured with `restart: unless-stopped`, so there's no need to (re)-start it after a reboot.
