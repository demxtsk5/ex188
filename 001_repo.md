# setup local repo

- install podman

```bash
dnf install podman
```

- setup local history

```bash
[root@r01 ~]# p run -d --name michas_reg -p 5000:5000 registry
Resolved "registry" as an alias (/etc/containers/registries.conf.d/000-shortnames.conf)
Trying to pull docker.io/library/registry:latest...
Getting image source signatures
Copying blob b98a2db964ee done   |
Copying blob 720f3032cd11 done   |
Copying blob d259642272e5 done   |
Copying blob 6e496f333012 done   |
Copying blob e961822193ae done   |
Copying config c9cf76bb10 done   |
Writing manifest to image destination
68ef77681117e42fbce9f00af2f1fd32e945e96506b04e3deebcae5b7b585547
[root@r01 ~]# p ps
CONTAINER ID  IMAGE                              COMMAND               CREATED        STATUS        PORTS                   NAMES
68ef77681117  docker.io/library/registry:latest  /etc/docker/regis...  6 seconds ago  Up 6 seconds  0.0.0.0:5000->5000/tcp  michas_reg
````

- add localhost:5000 as an insecure registry (in exam use registry:5000)
- make sure localhost:5000 is used before trying others  
  
```bash
vi /etc/containers/registries.conf

unqualified-search-registries = ["localhost:5000", "registry.access.redhat.com", "registry.redhat.io", "docker.io"]
[[registry]]
insecure = true
location = "localhost:5000"
```
  
- analyze images on server (not local)

```bash
man skopeo-inspect
skopeo inspect docker://docker.io/library/httpd
```

- pull image from history

```bash
podman pull httpd:2.4.61
```

- analyze local image (e.g. exposed ports, enviroment variables)

```bash
podman inspect httpd:latest
```
