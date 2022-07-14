# PostgreSQL:
## This will boot a PostgreSQL Docker Container

## Docker Compose:
```
version: '3'

services:

  db:
    image: mysql:5.7.23
    restart: always
    container_name: "mysql_5_7"
    environment:
      MYSQL_ROOT_PASSWORD: 123456
    ports:
      - 3306:3306
    volumes: 
      - ./data:/var/lib/mysql
```


### Deploy with docker compose

```
$ docker compose up -d
```

### Stop and remove the containers

```
$ docker compose down
```
