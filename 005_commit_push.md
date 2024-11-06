# Commit and push to localhistory

### Do the following with your newly created alp-httpd container:

- Execute an interactive shell (/bin/sh) in the alp-httpd container
- Change the text in /usr/local/apache2/htdocs/index.html from “It works!” to “It Twerks!”
- Use curl to test your changes.
- Commit the container to an image named registry:5000/httpd:twerks.
- Push your new image to the registry server (you can check this by visiting http://registry.do180.lab -- the page updates every minute)
- Kill your alp-httpd container and run a new one based on the twerks image using port 8008. Name it tw-httpd
