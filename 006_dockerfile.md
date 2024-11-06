# Containerfile
asap Dockerfile

Use the incomplete file located at /dockerfiles/nginx/Dockerfile to create a new image. It must meet these requirements:

- Pull from centos:8
- Install nginx
- Publish port 80 to the outside world
- Copy index.html and duffman.png into /usr/share/nginx/html directory
- Run the command nginx -g daemon off
- Tag this image as quay.io/YOURUSERNAME/duff-nginx:1.0 and push it to your quay.io account.
- Run a container in detached mode named duffman that publishes port 80 to 8989. Test it with curl localhost:8989
 