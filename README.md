# guacamole docker
Setting up guacamole docker composition for Linux

# Create certificate
``
chmod +x create_cert.sh
./create_cert.sh
``

# Generate database initialization script
``
docker run --rm guacamole/guacamole /opt/guacamole/bin/initdb.sh --postgres > ./postgres/initdb.sql
``

# Create database volume manually
``
docker volume create --name guacamole_guacamole_db
``

# Initialize database
``
docker run --rm -it --env-file ./.env -v guacamole_guacamole_db:/var/lib/postgresql/data:rw postgres:10-alpine
``

# Modify database
``
docker run --rm -it --user postgres:postgres --env-file ./.env -v /e/Projekte/guacamole_docker/postgres:/tmp:rw postgres:10-alpine /bin/sh
``
OR
``
docker run -d --name postgres -v guacamole_guacamole_db:/var/lib/postgresql/data:rw --user postgres:postgres --env-file ./.env postgres:10-alpine
docker cp ./postgres/initdb.sql postgres:/initdb.sql
docker exec -it --user postgres:postgres postgres /bin/sh
``
OR
``
docker create -it --name postgres_modification -v guacamole_guacamole_db:/var/lib/postgresql/data:rw --user postgres:postgres --env-file ./.env postgres:10-alpine /bin/sh
docker cp ./postgres/initdb.sql postgres_modification:/initdb.sql
docker start -i -a postgres_modification
``

# Change encoding
``
iconv -f UTF-16LE -t UTF-8 initdb.sql > /tmp/initdb_utf8.sql
``

# Run SQL script file
``
psql -d $POSTGRES_DB -a -f /tmp/initdb_utf8.sql
``

# Copy certificates and keys
``
docker volume create guacamole_nginx_certs
docker volume create guacamole_nginx_config
docker create -it --name="mydebian" -v guacamole_nginx_certs:/nginx_certs:rw -v guacamole_nginx_config:/nginx_config:rw debian:latest /bin/bash
docker cp ./reverseproxy/config/. mydebian:/nginx_certs
docker cp ./reverseproxy/ssl/. mydebian:/nginx_config
docker start -a -i mydebian
``

# Create a test container including it into a container
``
docker run -it --rm --network="guacamole_back" --name="mydebian" debian:latest /bin/bash
``

# Reach guacamole:
* https://{HOST_IP}/guacamole/guacamole/#/
* TODO: Better URL routing
* Default user & pass: guacadmin

# Links
* [Guacamole Proxy](https://guacamole.apache.org/doc/gug/proxying-guacamole.html)
* [Guacamole Docker](https://hub.docker.com/r/guacamole/guacamole/)
* [Nginx Docker](https://hub.docker.com/r/library/nginx/)
* [Guacd Docker](https://hub.docker.com/r/guacamole/guacd/)
* [Postgres Docker](https://hub.docker.com/_/postgres/)
