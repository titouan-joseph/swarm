# Traefik 

## Lunch

Needs :   
  - `services` directory with additional configuration files  
  - `acme.json` for certificats with 600 permissions  
  - `access.log` for log  
  - `log.log` for log  
  - `passwd` for authentication

Command to use : `docker stack deploy -c Docker-compose.yml traefik`

## Local server

### Add services in `services` directory with

```yaml
http :
  services :
    <ServiceName> :
      loadBalancer :
        servers :
          - url : "http:/<ip>:<port>/"
```

### Add router in `services` directory with

```yaml
http :
  routers :
    <RouterName> :
      rule : "Host(`<domaine.com>`)"
      service : "<Service to access>"
      tls : {}
```

## Docker container

### Docker compose for Swarm

Adding this lables :

```yaml
services: 
  <Container name>:
    deploy :
      labels:
        - "traefik.enable=true"
        - traefik.http.routers.viz.tls=true
        - "traefik.http.routers.viz.rule=Host(`<Domaine.com>`)"
        - "traefik.http.routers.viz.tls.certresolver=le"
        - "traefik.http.routers.viz.entrypoints=websecure"
        - "traefik.http.services.viz.loadbalancer.server.port=<port>" # If multiple ports on container
```

And adding this network : 

```yaml
networks:
  - traefik-public
```

### Docker service for Swarm

```bash
docker service create \
--name test \
--label "traefik.enable=true" \
--label "traefik.http.routers.helloworld.tls=true" \
--label "traefik.http.routers.helloworld.rule=Host(\`helloworld.cluster.revol.site\`)" \
--label "traefik.http.routers.helloworld.tls.certresolver=le" \
--label "traefik.http.routers.helloworld.entrypoints=websecure" \
--label "traefik.http.services.helloworld.loadbalancer.server.port=80" \
--network traefik-public \
nginx:alpine
```

## More

### Authentication

adding label : `traefik.http.routers.<RouterName>.middlewares=traefik-auth`