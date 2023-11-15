# MHK: migrating from mysql to mariaDB

From version 5.5 onwards MHK uses `mariadb` instead of `mysql`.

However if a previous `mysql` database is detected
and a version with `mariadb` was never run before,
MHK will use continue to use mysql.

It is recommended to use the mariadb version as the mysql version used (5.7) is no longer maintained.
 


There are two methods to migrate to `mariaDB`: 1-reimport the sources and identifications into
a fresh mariaDB database; 2-migrate the existing
`mysql` database to `mariaDB`.

The first method is more time consuming specially
if several users and `mhk` databases are involved.

The second method is simpler but it also can
trigger incompatibility problems if the existing
`mhk` database are old and not updated for a long
time.

In either case it is always possible to return
to the `mysql` database.

Also, in either case, it is highly recommended that
an updated version of `mhk` is used and that a login
in each user/database is done before the migration. 

This is 
because `mhk` does internal updating and fixing
of database problems when a user logs in. By logging
in each user the updating process is triggered.
It is not necessary to login more than one user for
each database (if more than one user use the same
database, it is enough to login once with one of
them).

To know which users are defined and which
databases they use do:

    mhk report

To know the database list:

    mhk db list


## Method 1: with version 5 running, export identifications and backup database
1. Check the databases in the current MHk instalation


        xserver:~ jrc$ mhk db list
        Running db command db list
        [+] Running 1/0
        ⠿ Container mhk-mysql-1  Running 0.0s
        ilhavo
        soure
        soure_editor
        toliveira_china_jesuitas
        ucprosop
        
2. Export current identifications as Kleio files
   1. For each database, login with an user that has admin rights
   2. In the tab "Identifications" select the separator "Export"
   3. Click on "Export identifications for all users"
   4. Check in "identifications" directory of the sources associated with each user to  verify that the identification files were exported
   5. Repeat this process for each database

3. Do a full dump of the database


        xserver:~ jrc$ mhk db dump
        Running db command db dump
        [+] Running 1/0
        ⠿ Container mhk-mysql-1  Running 0.0s
        Export will go to file mhk-home/system/db/mysql/backup/all_databases.
        Enter mysql root password when requested.
        Enter password: 
        -- Connecting to localhost...  

4. On a version 6 instalation
   
   1. Copy the full dump to  mhk-home/system/db/mysql/backup/
   2. Import from backup with

                mhk db import <FILE>

        for a list of files do just

                mhk db import

   3. After import from backup do 

                mhk db upgrade
                mh db fix-premissions


   4. Copy sources and users from version 5
   

## Method 2: export full database from mysql to mariadb


If you want to migrate the full database from mysql to mariadb
you can use the following commands:
   mhk use-mysql; mhk stop; mhk start
   mhk db dump
   mhk stop
   mhk use-mariadb
   mhk start
   mhk db import <dump file> # 'mhk db import' alone will list the dump files

if after the migration you have permission problems do:

   mhk db upgrade
   mhk db fix-permissions

You can always go back to the mysql version with

    mhk use-mysql
    mhk stop
    mhk start

It is recommended to use the mariadb version as the mysql version
used (5.7) is no longer maintained.
