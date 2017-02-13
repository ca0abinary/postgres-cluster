# postgres-cluster
A docker container which can act as primary or standby in a postgresql replication streaming cluster

### Origin
This container is based on the [offical postgresql docker container](https://hub.docker.com/_/postgres/), currently 9.6-alpine. If you would like to see how to extend this container, then please refer to that guide.

### Usage
This container can be used in the same manner as the [offical postgresql docker container](https://hub.docker.com/_/postgres/) with a couple exceptions:

1. The environment variable `PRIMARY=yes` must be specified for the primary container
2. The standby containers must be linked to the primary on the name `pg-primary`
3. There are a limit of 15 WAL slots, so a cluster size of 16 is the max without modifying anything

### Example usage

Starting a primary (for testing):
```docker run --rm -it -e PRIMARY=yes --name pg-primary ca0abinary/postgres-cluster```

Starting a standby (for testing):
```docker run --rm -it --link pg-primary:pg-primary ca0abinary/postgres-cluster```
