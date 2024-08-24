# Commands

For ginny bot

`docker service create --name ginnybot --env-file .env --restart-condition any 127.0.0.1:5000/ginnybot`

For registry

`docker service create --name registry --publish published=5000,target=5000 registry:2`

For machine a cafe bot  

`docker service create --name machineacafe --env-file .env --restart-condition any --mount type=bind,src=$(pwd)/deploy,dst=/bot/database 127.0.0.1:5000/machineacafe`

For bot zach

`docker service create --name botzach --env-file .env --restart-condition any 127.0.0.1:5000/bot_discord`

For astus bot

`docker service create --name astusbot --env-file .env --restart-condition any 127.0.0.1:5000/astusbot`

For portfolio

```bash
docker service create \
--name portfolio \
--label "traefik.enable=true" \
--label "traefik.http.routers.portfolio.tls=true" \
--label "traefik.http.routers.portfolio.rule=Host(\`titouan-joseph.cicorella.net\`) || Host(\`www.titouan-joseph.cicorella.net\`) || Host(\`tit.cicorella.net\`)" \
--label "traefik.http.routers.portfolio.tls.certresolver=le" \
--label "traefik.http.routers.portfolio.entrypoints=websecure" \
--label "traefik.http.services.portfolio.loadbalancer.server.port=80" \
--network traefik-public \
127.0.0.1:5000/portfolio:latest
```
