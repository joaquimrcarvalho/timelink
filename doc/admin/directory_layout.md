# Directory layout of timelink/mhk instalations

A single directory, called `mhk-home` (alternatively `timelink-home`) contains all that is necessary to run timelink. 

It contains the following subdirectories:

    
* `app` - Scripts and docker files necessary to run the application. 
   This directory is updated for each release.
* `system` - Configuration and support files for running the application. 
    * `logs` - location of log files
    * `conf` - configuration for the various services
        * `mhk_system.properties` file with global configuration of services, such as URLs for services
        * `kleio` (dir)
            * `stru` (dir)
                * `gacto2.str` file, with the sources schema)
            * `token_db` the database with user tokens
    * `db` - database related stuff including MySQL database files
        * `mhk` (dir)
            * contains mhk import reports (xrpt e xerr) dentro de diretorias tipo /system/db/mhk/imports/dbname/path_to_file
        * `mysql`
            * `backups` (dir) contains files created by database backup. Also location where `mhk` database commands look for SQL files to import.
            * `db` (dir) MySQL/MariaDB database storage directory, maps to /vat/lib/mysql
            * `init` (files for database initialization sql - sql, sql.gz e .sh - mapeia para /docker-entrypoint-initdb.d)
* `users`
    * user1
        * conf - configuration for this user
        * ids - backup of this user identification
        * backups - database backups for this user
    * user2
    * user3
* `projects` (previously named `sources`) See https://github.com/joaquimrcarvalho/timelink-sources-template for a template for each project
    * project_1
        * sources -- kleio sources
        * identifications -- identifications for this project (all users).
        * structures -- stru files to use with this community sources
        * database -- database related files, including backups and sqlite db files.
        * inferences -- inferred information, such as rules
        * kleio -- kleio-server working directory (created by kleio-server)
    * project_2
        * ...
    * project_3
        * ...