# guacamole docker
Setting up guacamole docker composition for Linux

# Initialize database
``
docker run --rm guacamole/guacamole /opt/guacamole/bin/initdb.sh --postgres > initdb.sql
``

# Links
* [Guacamole Proxy](https://guacamole.apache.org/doc/gug/proxying-guacamole.html)
* [Guacamole Docker](https://hub.docker.com/r/guacamole/guacamole/)
* [Nginx Docker](https://hub.docker.com/r/library/nginx/)
* [Guacd Docker](https://hub.docker.com/r/guacamole/guacd/)
