# Visualizer

## Lunch with docker Swarm as stack

`docker stack deploy -c Docker-compose.yml viz`  

Dashboard on `https://viz.cluster.revol.site`  

## Lunch with docker Swarm as service

```bash
docker service create \
--name viz \
--label "traefik.enable=true" \
--label "traefik.http.routers.helloworld.tls=true" \
--label "traefik.http.routers.helloworld.rule=Host(\`viz.cluster.revol.site\`)" \
--label "traefik.http.routers.helloworld.tls.certresolver=le" \
--label "traefik.http.routers.helloworld.entrypoints=websecure" \
--label "traefik.http.services.helloworld.loadbalancer.server.port=8080" \
--constraint=node.role==manager \
--mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
--network traefik-public \
alexellis2/visualizer-arm:latest
```