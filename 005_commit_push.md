# Commit and push to localhistory

### Do the following with your newly created alp-httpd container:

- Execute an interactive shell (/bin/sh) in the alp-httpd container
- Change the text in /usr/local/apache2/htdocs/index.html from “It works!” to “It Twerks!”
- Use curl to test your changes.
- Commit the container to an image named registry:5000/httpd:twerks.
- Push your new image to the registry server (you can check this by visiting http://registry.do180.lab -- the page updates every minute)
- Kill your alp-httpd container and run a new one based on the twerks image using port 8008. Name it tw-httpd

```bash
skopeo inspect docker://docker.io/library/httpd
podman pull docker.io/httpd:alpine3.20

p run -d --name alp-httpd -p 8008:80 docker.io/library/httpd:alpine3.20

curl localhost:8008

podman exec -it alp-httpd /bin/sh
cd htdocs
echo echo "<html><body><h1>It Twerks!</h1></body></html>" > index.html
exit

podman commit --author "mg0050" alp-httpd localhost:5000/httpd:twerks

podman push localhost:5000/httpd:twerks quay.io/mg0050/httpd:twerks
```
 
[Link to quay.io][quay.io]

[quay.io]: https://quay.io/repository/mg0050/httpd?tab=tags