# MHK command to create a new user

Get the GITURL and TOKEN ([see new user with sources in git](new_user_sources_in_git.md)).

Choose values for USER, DB and SOURCEDIR

    USER=myuser; DB=mydb;  SOURCEDIR=mysources

    mhk sources clone GITURL TOKEN SOURCEDIR
    mhk user create $USER  --database $DB --level 3 --sources $SOURCEDIR

## For  automatic import:

    mhk user properties $USER set mhk.import.auto yes
    mhk user properties $USER set mhk.import.auto.delay 120 # seconds

## Setting up a replica that pulls and synchronizes identifications


    mhk user properties $USER set mhk.import.auto yes-with-warnings; \
    mhk user properties $USER set mhk.import.auto.delay 120;  \
    mhk user properties $USER set mhk.git.pull.auto yes; \
    mhk user properties $USER set mhk.git.pull.auto.delay 10; \
    mhk user properties $USER set mhk.import.pull.before yes; \
    mhk user properties $USER set mhk.admin $USER; \
    mhk user properties $USER set mhk.import.authority.backup yes

## Set host in MHK

MHK can open a web browser from the command line 
if the WEBURL of the project is know:

```bash
mhk set-url www.mysite.org
```
