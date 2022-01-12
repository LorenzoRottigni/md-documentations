# Docker - CassandraDB Deployment

## Get cassandra image from docker.io:

`sudo docker pull cassandra`

## Run cassandra container from pulled image:

`docker run -d --name cassandra-container -p 9842:9842 cassandra`

## Enter container bash:

`docker exec --it cassandra-docker bash`

## Enter cassandra CLI (cqlsh):

`docker exec --it cassandra-docker cqlsh`

