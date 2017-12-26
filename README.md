# app

## dev locally

```bash
eval $(docker-machine env default)
docker-compose up
docker-compose down
```

Visit `http://192.168.99.100/` to see what's happening locally.

## deploy to swarm

1. `eval $(docker-machine env node-1)`
2. `./build`
3. `./deploy`

### creating nodes

``` bash
docker-machine create --driver digitalocean \
--digitalocean-image  ubuntu-16-04-x64 \
--digitalocean-private-networking \
--digitalocean-access-token $DOTOKEN node-1 &

docker-machine create --driver digitalocean \
--digitalocean-image  ubuntu-16-04-x64 \
--digitalocean-private-networking \
--digitalocean-access-token $DOTOKEN node-2 &

docker-machine create --driver digitalocean \
--digitalocean-image  ubuntu-16-04-x64 \
--digitalocean-private-networking \
--digitalocean-access-token $DOTOKEN node-3 &
```

### creating the swarm

After running the commands below you will get a command to run on the
worker nodes.

``` bash
docker-machine ls # to get the IP address of the nodes
docker swarm init --advertise-addr IP.A.DDRE.SS
```

Running commands on worker nodes is easy! Replace the node name below and the command. Boom.

``` bash
docker-machine ssh node-2 "ls"
```

## todo

- [ ] add tests
