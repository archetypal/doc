Images
======
```bash
docker images
docker build -t <image_tag_name> .
```

Containers
==========
```bash
docker ps -a
```

Create a container via docker run:

--name new container name
-p port in the form of external:docker
--rm remove once command terminates, can't be used with -d
-d daemon - headless start
-i - interactive
-t - terminal

```bash
docker run --rm -p 5000:5000 <image_tag_name>
```

Remote
```bash
docker exec -it <container> bash
```


Docker Machine
==============

```bash
docker-machine start default
```

If IP address changes or network connections change, regenerate certs.
```bash
docker-machine regenerate-certs <default>
```
Upgrade
```bash
docker-machine upgrade <default>
```

SSH into
--------
```
docker-machine ssh
```

Remote API
----------

Docker Windows Bash (from http://docs.docker.com/engine/reference/api/docker_remote_api/)
```
curl --insecure --cert ~/.docker/machine/certs/cert.pem --key ~/.docker/machine/certs/key.pem https://192.168.99.100:2376/images/json
```

curl --insecure --cert cert.pem --key key.pem https://192.168.99.100:2376/images/json

docker --tlsverify --tlscacert=ca.pem --tlscert=cert.pem --tlskey=key.pem -H=https://192.168.99.100:2376 version

docker --tlsverify --tlscacert=~/.docker/machine/certs/ca.pem --tlscert=~/.docker/machine/certs/cert.pem --tlskey=~/.docker/machine/certs/key.pem -H=tcp://192.168.99.100:2376 version

docker -H unix:///var/run/docker.sock

