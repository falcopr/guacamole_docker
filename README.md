# guacamole docker
Setting up guacamole docker composition for Linux

# Initialize database
``
docker run --rm guacamole/guacamole /opt/guacamole/bin/initdb.sh --postgres > initdb.sql
``

# Links
* https://hub.docker.com/r/guacamole/guacamole/
* https://hub.docker.com/r/library/nginx/
* https://hub.docker.com/r/guacamole/guacd/
