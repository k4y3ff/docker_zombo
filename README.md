# docker_zombo

Dockerfiles for ZomboDB with Postgres and Elasticsearch

Zombo + ElasticSearch
---------------------
Zombo + ES uses much of the outdated [ElasticSearch Dockerfile](https://github.com/dockerfile/elasticsearch), with additional commands to install the Zombo plugin.


Zombo + Postgres
----------------
Zombo + PG builds on the [Postgres Dockerfile](https://github.com/docker-library/postgres/blob/master/9.3/Dockerfile) and largely copies the [docker-entrypoint.sh](https://github.com/docker-library/postgres/blob/master/9.3/docker-entrypoint.sh) script with one addition to add `local_preload_libraries` to `postgresql.conf`


Build/Run/Exec Example
-----------------------

`docker build -t zombo_postgres .`

`docker build -t zombo_elastic .`

`docker run zombo_postgres`

`docker run zombo_elastic`

To get a shell in the above for tinkering:

`docker ps` to get your container_id

`docker exec -i -t container_id bash`
