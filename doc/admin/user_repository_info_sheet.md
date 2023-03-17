# User and repository sheet

Use this as a template to document internally each new project

# Information


| Variable	|  Description	            | Value |
|-----------|---------------------------|-------|
|GITURL	    | Git repository url	    |       |
|TOKEN	    | Git Personal access token |       |	
|USER	    | MHK new user name         |       |
|SOURCEDIR	| Local sources directory   |       |
|DB	        | MHK database name         |       |
|WEBURL     | Public URL (if any)       |       |


# Commands

    USER=myuser; DB=mydb;  SOURCES=mysources

    mhk sources clone GITURL TOKEN SOURCEDIR
    mhk user create $USER  --database $DB --level 3 --sources $SOURCEDIR

## For  automatic import:

    mhk user properties $USER set mhk.import.auto yes
    mhk user properties $USER set mhk.import.auto.delay 120 # seconds

## Setting up a replica that pulls and synchronizes identifications

    mhk user properties $USER set mhk.git.pull.auto yes
    mhk user properties $USER set mhk.git.pull.auto.delay 10 # seconds
    mhk user properties $USER set mhk.import.auto yes-with-warnings
    mhk user properties $USER mhk.import.auto.delay 120 # seconds
    mhk user properties $USER set mhk.import.pull.before yes
    mhk user properties $USER set mhk.import.authority.backup yes

## Set host in MHK

MHK can open a web browser from the command line 
if the WEBURL of the project is know:

```bash
mhk set-url www.mysite.org
```
