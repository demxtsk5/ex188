# start apache and create service
  
- pull latest httpd image
- publish port 80 on host 8080
- map local folder /web to /usr/local/apache2/htdocs
- set container name to reg-httpd
- make container start as service called reg-httpd.service
  
```bash
podman pull httpd:latest
podman images

mkdir /web
man semanage-fcontext

semanage fcontext -a -t httpd_sys_content_t "/web(/.*)?"
restorecon -R -v /web

podman run -d --name reg-httpd -p 8080:80 -v /web:/usr/local/apache2/htdocs:Z httpd
podman ps 

CONTAINER ID  IMAGE                           COMMAND           CREATED        STATUS        PORTS                 NAMES
37ef7ae36302  docker.io/library/httpd:latest  httpd-foreground  5 seconds ago  Up 5 seconds  0.0.0.0:8080->80/tcp  reg-httpd

curl localhost:8080
Mittwoch 6. November

man podman-generate-systemd
podman generate systemd --new --files --name reg-httpd
cp container-reg-httpd.service /usr/lib/systemd/system
systemctl daemon-reload
podman stop reg-httpd
systemctl enable --now container-reg-httpd.service
Created symlink /etc/systemd/system/default.target.wants/container-reg-httpd.service → /usr/lib/systemd/system/container-reg-httpd.service.

systemctl status container-reg-httpd.service
● container-reg-httpd.service - Podman container-reg-httpd.service
     Loaded: loaded (/usr/lib/systemd/system/container-reg-httpd.service; enabled; preset: disabled)
     Active: active (running) since Wed 2024-11-06 09:24:09 CET; 1min 0s ago
...
```

How to login into container?

```bash
podman exec -it reg-httpd /bin/bash
```

As ordinary user:

IMPORTANT: do ssh user@localhost

```bash
podman run -d --name test httpd
man podman-generate-systemd
podman generate systemd --new --files --name test
mkdir -p .config/systemd/user
mv container-test.service .config/systemd/user/.
loginctl enable-linger student
systemctl --user enable --now container-test.service

systemctl --user status container-test.service
● container-test.service - Podman container-test.service
     Loaded: loaded (/home/student/.config/systemd/user/container-test.service; enabled; preset: disabled)
     Active: active (running) since Wed 2024-11-06 09:34:49 CET; 4min 20s ago
```