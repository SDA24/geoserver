Install by docker:


Pulling stable version from docker hub.


    docker pull docker.osgeo.org/geoserver:2.26.0

Run the container:

    docker run -d -it --name geoserver --restart unless-stopped -p8080:8080 docker.osgeo.org/geoserver:2.26.0

Using your own data directory:

    docker run -it -p8080:8080 --mount type=bind,src=/MY/DATADIRECTORY,target=/opt/geoserver_data docker.osgeo.org/geoserver:2.26.0


---------------------------------------------------------------------------------------------

Install postgresql as a database:

Production env.

    docker run -d --name postgresql --restart unless-stopped -e ALLOW_EMPTY_PASSWORD=yes bitnami/postgresql:latest

----------------------------------------------------------------------------------------------

Switching database after connecting:

    \c database_name

List the tables:

    \dt

Create new user:

    CREATE USER <username> WITH PASSWORD '<password>';

Grant privilages to user:

    GRANT CONNECT ON DATABASE <database_name> TO <username>;
    GRANT USAGE ON SCHEMA public TO <username>;
    GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO <username>;

Change:

    ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO <username>;



List all users and roles in postgresql:

    SELECT rolname, rolsuper, rolcreaterole, rolcreatedb, rolcanlogin FROM pg_roles;

List privilages of each user:
    SELECT 
        grantee, 
        table_schema, 
        table_name, 
        privilege_type
    FROM 
        information_schema.role_table_grants
    ORDER BY 
        grantee, table_schema, table_name;

View privilages for a user on tables:

    SELECT 
        grantee, 
        table_schema, 
         table_name, 
         privilege_type
    FROM 
        information_schema.role_table_grants
    WHERE 
        grantee = '<username>';

Change password for specific user:

    ALTER USER <username> WITH PASSWORD '<new_password>';

------------------------------------------------------------------------------------------------

