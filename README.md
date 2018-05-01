# guacamole docker
Setting up guacamole docker composition for Linux

# Initialize database
``
docker run --rm guacamole/guacamole /opt/guacamole/bin/initdb.sh --postgres > initdb.sql
``

# Create a test container including it into a container
``
docker run -it --rm --network="guacamole_back" --name="mydebian" debian:latest /bin/bash
``

# Links
* [Guacamole Proxy](https://guacamole.apache.org/doc/gug/proxying-guacamole.html)
* [Guacamole Docker](https://hub.docker.com/r/guacamole/guacamole/)
* [Nginx Docker](https://hub.docker.com/r/library/nginx/)
* [Guacd Docker](https://hub.docker.com/r/guacamole/guacd/)
* [Postgres Docker](https://hub.docker.com/_/postgres/)
