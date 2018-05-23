# Prerequisites
1. Install `docker`
2. Install `docker-compose`
3. **TL;DR**: Start containers with `docker-compose up` or `docker-compose up -d` (More details: CLI Cheat Sheet)

# Some basic stuff for THIS docker-compose
## Container Composition
There are 3 containers defined:
* `mysql-dev`: This container starts a mysql instance on a specific host port. The root password, user, user password and database are defined in the `environment` section. The `/var/lib/mysql` folder of the container is mapped to the `data` folder on the host. The `my.cnf` file on the host will be placed in the container after startup.
* `client`: This container is an optional shell based mysql client, that allows you to connect to the database with the given user and password defined in the `mysql-dev` container. Thats why the `client` container depends on the `mysql-dev` container.
* `adminer`: This container helps to administrate running database server instances with the help of the adminer database management software.

## Container Usage
* `mysql-dev`: Just start the container and use it like a regular mysql server instance exposed through a specific port. (MySQL Workbench, PowerShell, Terminal, ...)
* `client`: To use this container, the `mysql-dev` container has to be up and running. Since this precondition is fulfilled just use this command to access the database through the `client` container: `docker-compose run --rm client`
* `adminer`: Inside a docker-compose network, all running containers, that expose a service through a given port, will have their own domain name. Thats why the database of the `mysql-dev` container will be available through the servername `mysql-dev` and the defined environment variables. This service will be exposed on a specific port on localhost and can be accessed via `localhost:<port>`

# docker-compose
## Basic Stuff
* Port syntax: `<Host Port>:<Container Port>`

## CLI Cheat Sheet
* start containers: `docker-compose up`
* start containers in background: `docker-compose up -d`
* stop containers: `docker-compose kill`
* force rebuild of Dockerfiles: `docker-compose up -d --build`
* remove stopped containers: `docker-compose rm`
* see list of running containers: `docker ps`
* ssh to the container: `docker exec -ti [NAME] bash`
