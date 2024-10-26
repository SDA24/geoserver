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

## 2. Backup of config files and layers:

Specifying the path to store layers and other information through the geoserver panel.  
Transfer the backup folder to **another** server:  

```bash
scp -r /path/to/backup/geoserver_data username@remote_server:/path/to/remote/backup/

```
**username**: Your username on the destination server.  
**remote_server**: IP address or domain name of the destination server. 
**/path/to/remote/backup/**: Destination path on another server.  


