# Mongo Cluster:
## This will boot 4 containers: 
- 3 Mongo shards in a cluster
- 1 Mongo (Mongosetup / balancer) to issue mongo commands to others

## Docker Compose:
```
version: "2.2"
services:
  mongo3:
    image: mongo:3.2
    restart: always
    entrypoint: [ "/usr/bin/mongod", "--replSet", "rs", "--rest", "--httpinterface" ]

  mongo2:
    image: mongo:3.2
    restart: always
    entrypoint: [ "/usr/bin/mongod", "--replSet", "rs", "--rest", "--httpinterface" ]

  mongo1:
    image: mongo:3.0
    restart: always
    entrypoint: [ "/usr/bin/mongod", "--replSet", "rs", "--rest", "--httpinterface" ]

  mongosetup:
    image: mongo:3.0
    volumes:
      - ./scripts:/scripts
    restart: always
    entrypoint: [ "bash", "/scripts/mongosetup.sh" ]
```


### Deploy with docker compose

```
$ docker compose up -d
```

### Stop and remove the containers

```
$ docker compose down
```
