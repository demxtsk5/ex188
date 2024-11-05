### setup local repo

- install podman
- setup local history
- add localhost:5000 as an insecure registry (in exam use registry:5000)
- make sure localhost:5000 is used before trying others  

```bash
dnf install podman
```
  
```bash
vi /etc/containers/registries.conf

unqualified-search-registries = ["localhost:5000", "registry.access.redhat.com", "registry.redhat.io", "docker.io"]
[[registry]]
insecure = true
location = "localhost:5000"
```
