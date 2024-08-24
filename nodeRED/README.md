# NodeRED

## Lance un conteneur docker

Les mapping suivant seront fait :

- Publication du port 1880 sur la machine host
- Création d'un volume docker ``myNodeREDdata``

Le conteneur est nommé ``mynodered``

```bash
docker run -it -p 1880:1880 -v myNodeREDdata:/data --name mynodered nodered/node-red:latest-minimal
```

## Activer l'authtentication

Dans le fichier ``settings.js`` qui se trouve :

- dans le conteneur : ``/data/settings.js``
- sur l'host : ``/var/lib/docker/volumes/myNodeREDdata/_data/settings.js``

Il faut :

1) Decommenter les lignes

```javascript
    adminAuth: {
        type: "credentials",
        users: [{
            username: "admin",
            password: "$2a$08$zZWtXTja0fB1pzD4sHCMyOCMYz2Z6dNbM6tl8sJogENOMcxWV9DN.",
           permissions: "*"
        }]
    },

```

1) Changer le nom d'utilisateur
1) Changer le mot de passe, cela peut se faire utiliser  la commande ``docker run --rm -it --entrypoint /usr/src/node-red/node_modules/.bin/node-red-admin nodered/node-red:latest-minimal hash-pw`` pour obtenir le hash du mot de passe

## Probleme de Simlink

1) Recuper la commande npm dans l'output de l'interface nodeRED
1) Lancer un shell sur le conteneur. Sur le noeud du cluster swarm lancer la commande ``docker exec -it nodered.nodred.1.[...] bash``
1) Se deplacer dans le dossier ``/data``
1) Lancer la commande npm avec le flag ``--no-bin-links`` en plus
1) Relancer l'installation dans l'interface nodeRED
