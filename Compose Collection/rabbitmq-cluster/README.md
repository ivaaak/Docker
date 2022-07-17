# RabbitMQ Cluster:
 This will boot a Cluster of 3 RabbitMQ Docker Containers which are interconnected.

# What is cluster in RabbitMQ?
 A RabbitMQ cluster is a logical grouping of one or several nodes, each sharing users, virtual hosts, queues, exchanges, bindings, runtime parameters and other distributed state.

## Docker Compose:
```
version: '3'

services:
  rabbitmq1:
    image: rabbitmq:3.7-management
    hostname: rabbitmq1
    environment:
      - RABBITMQ_ERLANG_COOKIE=testCookie
      - RABBITMQ_DEFAULT_USER=root
      - RABBITMQ_DEFAULT_PASS=123456
      - RABBITMQ_DEFAULT_VHOST=/
    ports:
      - "5672:5672"
      - "15672:15672"
    volumes:
      - ./rabbitmq1:/var/lib/rabbitmq
      
  rabbitmq2:
    image: rabbitmq:3.7-management
    hostname: rabbitmq2
    depends_on:
      - rabbitmq1
    environment:
      - RABBITMQ_ERLANG_COOKIE=testCookie
    volumes:
      - ./cluster-entrypoint.sh:/usr/local/bin/cluster-entrypoint.sh
      - ./rabbitmq2:/var/lib/rabbitmq
    entrypoint: /usr/local/bin/cluster-entrypoint.sh
    ports:
      - "5673:5672"
      
  rabbitmq3:
    image: rabbitmq:3.7-management
    hostname: rabbitmq3
    depends_on:
      - rabbitmq1
    environment:
      - RABBITMQ_ERLANG_COOKIE=testCookie
    volumes:
      - ./cluster-entrypoint.sh:/usr/local/bin/cluster-entrypoint.sh
      - ./rabbitmq3:/var/lib/rabbitmq
    entrypoint: /usr/local/bin/cluster-entrypoint.sh
    ports:
      - "5675:5672"
```


### Deploy with docker compose

```
$ docker compose up -d
```

### Stop and remove the containers

```
$ docker compose down
```
