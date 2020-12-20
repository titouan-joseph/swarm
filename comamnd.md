For ginny bot  

`docker service create --name ginnybot --env-file .env --restart-condition any 127.0.0.1:5000/ginnybot`

For registry   

`docker service create --name registry --publish published=5000,target=5000 registry:2`

For machine a cafe bot  

`docker service create --name machineacafe --env-file .env --restart-condition any --mount type=bind,src=$(pwd)/deploy,dst=/bot/database 127.0.0.1:5000/machineacafe`

