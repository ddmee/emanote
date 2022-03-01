# Docker container access ports on host

Say you're running a docker container, like nginx proxy manager, and you need the container to be able to access a port on the host. How do you do it?

(Say you want the nginx proxy manager to reverse proxy to a port on the host rather than in another container)


[This stackoverflow question](https://stackoverflow.com/questions/31324981/how-to-access-host-port-from-docker-container#43541732) holds the answers.

In particular, you can give the container general access to the host's port with:

```sh
docker run --net="host" ...
```

Then localhost in your docker container will point to your docker host.

In docker-compose this setting the [network mode](https://docs.docker.com/compose/compose-file/compose-file-v3/#network_mode) to host.

```docker-compose
  proxy:
    image: jc21/nginx-proxy-manager:latest
    network_mode: host
```

Though you cannot combine `network_mode` with `networks`.

So perhaps a better way is to use the special DNS name `host.docker.internal` which resolves to the internal IP address of the host.

#docker
