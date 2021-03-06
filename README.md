# app

[Read my blog post about this repo](https://levi.lol/docker-explained-for-php-developers-in-2018/).

## dev locally

```bash
eval $(docker-machine env default)
docker-compose up
```

Visit `http://192.168.99.100/` to see what's happening locally.

```bash
docker-compose down
```

Now you've taken down the stack.

## building the swarm

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

## deploy to swarm

1. `eval $(docker-machine env node-1)`
2. `./build`
3. `./deploy`

## faq

**toc**

1. [can't join swarm](https://github.com/levilol/php-docker#cant-join-swarm)
2. [mounting directory as file](https://github.com/levilol/php-docker#mount-directory-as-file)

### can't join swarm

If you get the following error message follow the solution below.

```
this node is not a swarm manager. Use "docker swarm init" or "docker swarm join" to connect this node to swarm and try again
```

**solution:** run `eval $(docker-machine env node-1)` and try again.

### mount directory as file

The following error may have more than one solution.

```
ERROR: for phpdocker_web_1  Cannot start service web: OCI runtime create failed: container_linux.go:295: starting container process caused "process_linux.go:399: container init caused \"rootfs_linux.go:57: mounting \\\"/Users/levidurfee/Projects/levilol/php-docker/docker/nginx/nginx.key\\\" to rootfs \\\"/var/lib/docker/aufs/mnt/6d22d8efdec1944f3e76ce79ed2ce60aa81aa358e080f22929619d90c21a4825\\\" at \\\"/var/lib/docker/aufs/mnt/6d22d8efdec1944f3e76ce79ed2ce60aa81aa358e080f22929619d90c21a4825/etc/nginx/nginx.key\\\" caused \\\"not a directory\\\"\"": unknown: Are you trying to mount a directory onto a file (or vice-versa)? Check if the specified host path exists and is the expected type
```

**solution:** run `eval $(docker-machine env default)` and try again.

## demo

Instead of paying for the Droplets to host this sample app I decided to record my terminal while I curl'd the app.

[![asciicast](https://asciinema.org/a/8KJoYkENCrVAHjOb1bf4wYLq7.png)](https://asciinema.org/a/8KJoYkENCrVAHjOb1bf4wYLq7)
