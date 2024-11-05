# setup local repo

- install podman

```bash
dnf install podman skopeo
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

- analyze local image (e.g. exposed ports, enviroment variables)

```bash
podman inspect httpd:latest
```

- pull image from history

```bash
[root@r01 ~]# p pull docker.io/library/mysql:latest
Trying to pull docker.io/library/mysql:latest...
Getting image source signatures
Copying blob 806ebf9b9401 done   |
Copying blob 8b4274ea61c5 done   |
Copying blob 08ba006fa9b4 done   |
Copying blob 92a1aa4ee2ea done   |
Copying blob df48654477e3 done   |
Copying blob a3bc7a62e19a done   |
Copying blob b037f0555e71 done   |
Copying blob 0cace4982789 done   |
Copying blob 29ead6e17e26 done   |
Copying blob d624aa804ccd done   |
Copying config 22aaacaafc done   |
Writing manifest to image destination
22aaacaafc0e7ec1fe9dde21dcc39fd815cec2f4c58a07b2bbe25410fc223203
[root@r01 ~]# p images
REPOSITORY                  TAG         IMAGE ID      CREATED        SIZE
docker.io/library/mysql     latest      22aaacaafc0e  3 weeks ago    642 MB
docker.io/library/registry  latest      c9cf76bb104e  13 months ago  25.5 MB
```
