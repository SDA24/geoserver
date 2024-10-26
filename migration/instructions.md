## 1. Backing up the existing database:

```bash
pg_dump -U <username> -W -F c -b -v -f /path/to/backup.sql <database_name>

```

**&lt;username&gt;** : is your database user name.  
**-W** : This switch will prompt you for a password. Enter the password for the user you entered.  
**-F c** : Specifies the format as custom, allowing for flexible restoration.  
**-b** : Includes large objects in the backup.  
To find out if there are Large Objects (LO) in your database, you can use a simple SQL query in PostgreSQL that directly checks the system table for Large Objects.

```bash		 
SELECT EXISTS (SELECT 1 FROM pg_largeobject);

```

				 
**-v** : Enables verbose mode, showing detailed operation logs.  
**-f** : Specifies the output file path.  
**&lt;database_name&gt;**: 

```bash
pg_dumpall -U <username> -W -f /path/to/backup_all.sql

```

***

**All databases**: If you need a complete backup of all databases and settings, **pg_dumpall** is a good option.

```bash
pg_dumpall -U <username> -W -f /path/to/backup_all.sql

```
***

## 2. Backup of postgresql data and config files and layers:

Specifying the path to store layers and other information through the geoserver panel.  
Transfer the backup folder to **another** server:  

```bash
scp -r /path/to/backup_all.sql username@remote_server:/

```

```bash
scp -r /path/to/backup/geoserver_data username@remote_server:/path/to/remote/backup/

```
**username**: Your username on the destination server.  
**remote_server**: IP address or domain name of the destination server. 
**/path/to/remote/backup/**: Destination path on another server.  

***

## 3. Setting up PostgreSQL on Docker:  

https://github.com/SDA24/geoserver/blob/install/Installer/README.md

***

Use the **docker cp command** to copy the file directly to the container.

```bash
docker cp /path/to/backup.sql postgresql:/backup_all.sql

```

Then inside the container, reset the backup file:

```bash
docker exec -it -u root postgresql bash

```

```bash
psql -U postgres -f /backup_all.sql

```
## 4. Setting up geoserver on Docker:  

Create specific volume by docker:

```bash
docker volume create geoserver_data

```
Running the GeoServer container:

https://github.com/SDA24/geoserver/blob/install/Installer/README.md

**Copy data to the container**: After your GeoServer container is running, you can **copy data** from the host to the container using the **docker cp command**. Assuming your data is in /path/to/backup/geoserver_data, run the following command:

```bash
docker cp /path/to/backup/geoserver_data/. geoserver:/opt/geoserver/data_dir/

```

***

## 5. PostgreSQL connection settings:

Enter the GeoServer user interface (http://geoserver-ip-address:8080/geoserver) and in the Stores section, by creating a new PostGIS Store, enter the PostgreSQL connection settings using the new configuration.
