## Compose MongoDB Docker Container.


[_compose.yaml_](compose.yaml)
```
# Use root/example as user/password credentials
version: '3.1'

services:

  mongo:
    image: mongo
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: example

  mongo-express:
    image: mongo-express
    restart: always
    ports:
      - 8081:8081
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: root
      ME_CONFIG_MONGODB_ADMINPASSWORD: example
      ME_CONFIG_MONGODB_URL: mongodb://root:example@mongo:27017/

```
The compose file defines a MongoDB Container.


## Deploy with docker compose

```
$ docker compose up -d
2.1: Pulling from library/mongo
```

Stop and remove the containers

```
$ docker compose down
```
