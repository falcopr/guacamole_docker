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
docker run --rm -it --env-file ./.env -v guacamole_db_guacamole_db:/var/lib/postgresql/data:rw postgres:10-alpine
``

# Modify database
``
docker run --rm -it --user postgres:postgres --env-file ./.env -v /e/Projekte/guacamole_docker/postgres:/tmp:rw postgres:10-alpine /bin/sh
``
OR
``
docker create -it --name postgres_modification -v guacamole_db_guacamole_db:/var/lib/postgresql/data:rw --user postgres:postgres --env-file ./.env postgres:10-alpine /bin/sh
docker cp ./postgres/initdb.sql postgres_modification:/initdb.sql
docker start -i -a postgres_modificationdocker
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
