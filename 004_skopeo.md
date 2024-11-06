# Skopeo

Use skopeo to find all of the tags associated with httpd on the docker.io server. Create and run a container with the following parameters:

- Use an httpd image from docker.io that is NOT tagged with latest
- Publish port 80 on 8008
- Give the container the name alp-httpd
- Run the container in detached mode

```bash
man skopeo-inspect
skopeo inspect docker://docker.io/library/httpd 
{
    "Name": "docker.io/library/httpd",
    "Digest": "sha256:bbea29057f25d9543e6a96a8e3cc7c7c937206d20eab2323f478fdb2469d536d",
    "RepoTags": [
        ...
        "2.4.62",
        "2.4.62-alpine",
        "2.4.62-alpine3.20",
        "2.4.62-bookworm",
        "alpine",
        "alpine3.13",
        "alpine3.14",
        "alpine3.15",
        "alpine3.16",
        "alpine3.17",
        "alpine3.18",
        "alpine3.19",
        "alpine3.20",
        "bookworm",
        "bullseye",
        "buster",
        "latest"
        ...
    ]
}
```

```bash
podman run --name=alp-httpd -d -p 8008:80 docker.io/library/httpd:buster

podman ps

CONTAINER ID  IMAGE                           COMMAND           CREATED        STATUS        PORTS                 NAMES
0a0fd6163131  docker.io/library/httpd:buster  httpd-foreground  2 seconds ago  Up 2 seconds  0.0.0.0:8008->80/tcp  alp-httpd
```
