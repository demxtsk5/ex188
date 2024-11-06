# Skopeo

Use skopeo to find all of the tags associated with httpd on the registry.do180.lab server. Create and run a container with the following parameters:

- Use an httpd image from registry.do180.lab that is NOT tagged with latest
- Publish port 80 on 8008
- Give the container the name alp-httpd
- Run the container in detached mode

```bash
man skopeo-inspect
skopeo inspect docker://registry.do180.lab:5000/httpd 
{
    "Name": "registry.do180.lab:5000/httpd",
    "Digest": "sha256:fd54136dc090c0de9a65f7d4e31f18864b7a13db852a58e14899bbee84188837",
    "RepoTags": [
        "latest",
        "2.4-alpine"
    ]
}
```

```bash
podman run --name=alp-httpd -d -p 8008:80 registry.do180.lab:5000/httpd:2.4-alpine

podman ps
CONTAINER ID  IMAGE                                     COMMAND           CREATED         STATUS             PORTS                   NAMES
ad5a760e4af7  registry.do180.lab:5000/httpd:2.4-alpine  httpd-foreground  25 seconds ago  Up 24 seconds ago  0.0.0.0:8008->80/tcp    alp-httpd
```
