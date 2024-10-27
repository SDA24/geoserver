Install by docker:


Pulling stable version from docker hub.


    docker pull docker.osgeo.org/geoserver:2.26.0

Run the container:

    docker run -d -it --name geoserver --env INSTALL_EXTENSIONS=true --env STABLE_EXTENSIONS="ysld,h2" --restart unless-stopped -p8080:8080 docker.osgeo.org/geoserver:2.26.0

Using your own data directory:

    docker run -d -it --env INSTALL_EXTENSIONS=true --env STABLE_EXTENSIONS="ysld,h2" --restart unless-stopped -p8080:8080 -v geoserver_data:/opt/geoserver_data docker.osgeo.org/geoserver:2.26.0


---------------------------------------------------------------------------------------------

Install postgresql as a database:

Production env.

    docker run -d --name postgresql --restart unless-stopped -v postgres_data:/var/lib/postgresql/data -e ALLOW_EMPTY_PASSWORD=yes bitnami/postgresql:latest

----------------------------------------------------------------------------------------------
