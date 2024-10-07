Install by docker:


Pulling stable version from docker hub.


    docker pull docker.osgeo.org/geoserver:2.26.0

Run the container:

    docker run -d -it -p8080:8080 docker.osgeo.org/geoserver:2.26.0

Using your own data directory:

    docker run -it -p8080:8080 --mount type=bind,src=/MY/DATADIRECTORY,target=/opt/geoserver_data docker.osgeo.org/geoserver:2.26.0


---------------------------------------------------------------------------------------------

Install postgresql as a database:

Production env.

    docker run -d --name postgresql -e ALLOW_EMPTY_PASSWORD=yes bitnami/postgresql:latest
