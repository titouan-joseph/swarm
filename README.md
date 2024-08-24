# swarm

Cluster docker swarm

Pour lancer les stack utiliser la commande suivante :

```bash
eval $(< .env) docker stack deploy --compose-file docker-compose.yml stack-name
```

## Liste des services

- Traefik
- Registry
- NodeRED
- minio
- neonlink
