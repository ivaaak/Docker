# RabbitMQ:
## This will boot a RabbitMQ Docker Container

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
