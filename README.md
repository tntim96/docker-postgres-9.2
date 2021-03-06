dockerfiles-centos-postgres
===========================

Dockerfile to build PostgreSQL with PostGIS on CentOS 7

Ported from https://github.com/CentOS/CentOS-Dockerfiles/tree/master/postgres/centos7

Setup
-----

To build the image

    # docker build --rm -t tntim96/postgresql-postgis:9.2 .


Launching PostgreSQL
--------------------

#### Quick Start (not recommended for production use)

    docker run --name=postgresql -d -p 5432:5432 tntim96/postgresql-postgis


To connect to the container as the administrative `postgres` user:

    docker run -it --rm --volumes-from=postgresql tntim96/postgresql-postgis:9.2 sudo -u
    postgres -H psql


Creating a database at launch
-----------------------------

You can create a postgresql superuser at launch by specifying `DB_USER` and
`DB_PASS` variables. You may also create a database by using `DB_NAME`.

    docker run --name postgresql -d \
    -e 'POSTGRES_USER=pg_admin' \
    -e 'POSTGRES_PASSWORD=pg_admin' \
    -e 'POSTGRES_DB=pg_admin' \
    tntim96/postgresql-postgis:9.2

To connect to your database with your newly created user:

    psql -U username -h $(docker inspect --format {{.NetworkSettings.IPAddress}} postgresql)
