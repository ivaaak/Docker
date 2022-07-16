# RabbitMQ:
## This will boot a RabbitMQ Docker Container

#What is RabbitMQ?

RabbitMQ is open source message broker software (sometimes called message-oriented middleware) that implements the Advanced Message Queuing Protocol (AMQP). The RabbitMQ server is written in the Erlang programming language and is built on the Open Telecom Platform framework for clustering and failover. Client libraries to interface with the broker are available for all major programming languages.

## Docker Compose:
```
version: '3'

services:
  rabbit:
    image: rabbitmq:3.7-management
    hostname: rabbit
    container_name: "rabbitmq_3_7"
    restart: always
    ports:
      - "5672:5672"
      - "15672:15672"
    environment:
      - RABBITMQ_DEFAULT_USER=root
      - RABBITMQ_DEFAULT_PASS=123456
    volumes:
      - ./data:/var/lib/rabbitmq

```


### Deploy with docker compose

```
$ docker compose up -d
```

### Stop and remove the containers

```
$ docker compose down
```
