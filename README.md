# docker_zombo

Dockerfiles for ZomboDB with Postgres and Elasticsearch

Zombo + ElasticSearch
---------------------
Zombo + ES uses much of the outdated [ElasticSearch Dockerfile](https://github.com/dockerfile/elasticsearch), with additional commands to install the Zombo plugin.


Zombo + Postgres
----------------
Zombo + PG builds on the [Postgres Dockerfile](https://github.com/docker-library/postgres/blob/master/9.3/Dockerfile) and largely copies the [docker-entrypoint.sh](https://github.com/docker-library/postgres/blob/master/9.3/docker-entrypoint.sh) script with one addition to add `local_preload_libraries` to `postgresql.conf`


Building/Running
-----------------

`docker-compose build`

`docker-compose up`

If you have existing containers resulting in `docker-compose up` failing, try `docker-compose rm -f` to remove all containers.

Creating Zombo Indices
----------------------
Zombo requires you to specify the endpoint where ES can be reached when creating an index. When Docker starts up the service, it will map the service/container name to the exposed ports via `/etc/hosts`. You can get this name as follows:

```
bash-3.2$ docker-compose ps
            Name                          Command               State                       Ports
----------------------------------------------------------------------------------------------------------------------
dockerzombo_zombo_elastic_1    /elasticsearch/bin/elastic ...   Up      0.0.0.0:9200->9200/tcp, 0.0.0.0:9300->9300/tcp
dockerzombo_zombo_postgres_1   /zombo-entrypoint.sh postgres    Up      0.0.0.0:5432->5432/tcp
```

Then to create your index:
```sql
CREATE INDEX idx_zdb_products
          ON products
       USING zombodb(zdb(products))
        WITH (url='http://dockerzombo_zombo_elastic_1:9200/');
```