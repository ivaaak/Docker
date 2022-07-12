# Mongo + Elasticsearch + Kibana
## This will start 5 nodes:
- Mongo server as the only member of the cluster
- Mongosetup will init mongo as the master node
- Elasticsearch will serve as the index search db
- Kibana will serve as the web ui of elasticsearch
- Mongo-connector will pipeline mongodb content to the elasticsearch

[_compose.yaml_](compose.yaml)
```
mongo:
  image: mongo:3.0
  hostname: mongo
  mem_limit: 1024m
  expose:
    - "27017"
    - "28017"
  restart: always
  entrypoint: [ "/usr/bin/mongod", "--replSet", "rs", "--smallfiles", "--httpinterface", "--rest" ]

mongosetup:
  image: yeasy/mongosetup
  mem_limit: 1024m
  links:
    - mongo:mongo

elasticsearch:
  image: elasticsearch:1.7
  mem_limit: 1024m
  #volumes:
    #- /opt/data/elasticsearch:/usr/share/elasticsearch/data
  expose:
    - "9200"
    - "9300"

kibana:
  image: kibana:4.1
  ports:
    - "5601:5601"
  links:
    - elasticsearch:elasticsearch

mongoconnector:
  image: yeasy/mongo-connector
  links:
    - elasticsearch:elasticsearch
    - mongo:mongo

```


## Deploy with docker compose

```
$ docker compose up -d
```

Stop and remove the containers

```
$ docker compose down
```
