# MHK: migrating from version 5 to version 6

## With version 5 running, export identifications and backup database
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
   

