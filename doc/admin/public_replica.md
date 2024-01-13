# Setting up a public replica

## Multiple versions of a database from the same sources

In Timelink/MHK based projects it is sometimes desirable to have more than one copy of the database. 

A common situation is that of having a "work in progress” database, used by the contributors to the project, and a “public” version available in the Internet.

The public version provides an always available version of the database, containing only verified sources and identifications. 

The private  version will contain "in progress" versions of the database, that correspond to different stages of the process of inputing sources and identifying people and other entities.

## Editor versions and Server versions

We call "Editor" a version of a Timelink database that is used to translate and input sources in a database that is not normally available to the public. 

In most cases, users with Editor roles will run Timelink/MHK on a local or portable machine that is not always connected to the internet. Editor versions normally contain "work in progress", as sources are imported, vocabularies are checked and corrections are made.  Also "Editor" versions are used to make the identifications of entities.

We call "Server" a version of a Timelink database one that is public, and will  normally contain verified and correct versions of the sources and identifications.

## Git as the synchronisation mechanism

Timelink uses Git to achieve database replication and versioning. 

A common Git repository is used to sincronize Timelink/MHK Editor databases with server databases.

Following normal git workflow models, Editor users will push to the repository the validated sources and identifications. Validated
means that they were translated with no errors and any warnings
were analysed. 

Note that since July 2020 identification information is saved in Kleio files, which are stored along with source files, in a special directory called "identifications". The user must trigger the
export of identifications in the "linking" tab.

The Git repository contains not only the Kleio notation files (extension ".cli") but also the files produced by the translation process (.xml, .rpt and .err files). This set of files allows Timelink to identify the ones that are ready to be imported, because they were translated with no errors.

The Server version of the database periodically checks the git repository for new versions of source and identification files. When new versions or new files are found, they are "pulled" from the remote repository and imported.

_The Server version should not be used to make translations_. The Editor pushes to the git repository the files already translated
with no errors. A properly configured Server
replica will automatically import new translations obtained from the git repository without human intervention.

 Files are imported by change date, so that the most recently changed are imported last. 

## Editors and Servers as users

In practice "Editor" and "Server" are associated with different users of a database. 

An "Editor" user is a normal user with level 3 privileges. The sources associated with the user must be managed by a git repository, and the user must have "push" privileges to that repository.

A "Server" user is a user also with level 3 privileges but with some extra properties that trigger the automatic "pull" and import of files from the same repository.

The normal setup is to have Editor users in a local machine and a Server user  in a server machine available in the Cloud. But it is possible for the same Timelink/MHK installation, on the same machine to have Editor users and Server users. 

We recommend to name users accordingly to avoid confusion. For instance, for a database called "soure" an editor user could be named "soure-editor" and a server user "soure-server"

## Setting up a dual Editor - Server install

We are going to create an editor user and a server user for the sources in the repository https://github.com/joaquimrcarvalho/soure-fontes.git

In this example we use the same machine as Editor and Server.

In normal real life situations the Editor will be setup in 
a personal machine and the Server in a virtual machine or server
always available in the Internet.

### Check-out two copies of the repository into mhk-home/sources

```bash
cd ~/mhk-home/sources
git clone https://github.com/joaquimrcarvalho/soure-fontes.git soure-server
git clone https://github.com/joaquimrcarvalho/soure-fontes.git soure-editor
``````

We now have two copies of the repository in directories `mhk-home/sources/soure-server` and `mhk-home/sources/soure-editor``

### Creating the editor user

```bash
mhk user create soure-editor --database soure_editor --level 3 --sources soure-editor
```
>(Enter and confirm password, hit return when asked about local path to sources directory. Note underscore in database name "soure_editor"). Database names should not contain hifens.

### Creating the server user (normally in a server machine on the cloud):

```bash
mhk user create soure-server --database soure_server --level 3 --sources soure-server
```

### Configure the server user to pull new versions from git and auto import them

```bash
#set auto import of new files
mhk user properties soure-server set mhk.import.auto yes
```

>Important: if in the editor database you are importing files translated with warnings then the server database must also import files with warning, which is NOT the default bewhaviour. See bellow.


### Set interval between the scheduling of imports (not the actual end of imports) in seconds

```bash
mhk user properties soure-server set mhk.import.auto.delay 300
```

### make auto import do a git pull before import

```bash
mhk user properties soure-server set mhk.import.pull.before yes
```

>Note: You can also set automatic import in an editor user. This would save the time to go to the web interface and trigger the import of new translations manually. In that case it is enough to set 

```bash
mhk user properties soure-server set mhk.import.auto yes
```
This only imports automatically files translated with no errors and no warnings. 
To also import files with translation warnings do, at your own risk:

```bash
mhk user properties soure-editor set mhk.import.auto=yes-with-warnings
```
# set to a reasonable interval in seconds
```bash
mhk user properties soure-editor set mhk.import.auto.delay 120
```

### Make import of identification backups automatic

```bash
mhk user properties soure-server set mhk.import.authority.backup yes
```

 Other Git related properties

```bash
# set auto git pull
mhk user properties soure-server set mhk.git.pull.auto yes

# set the git URL
mhk user properties soure-server set mhk.git.origin https://github.com/joaquimrcarvalho/soure-fontes.git

# set the interval in minutes between checks of the repository. 
mhk user properties soure-server set mhk.git.pull.auto.delay 5

# optionally you can special a branch of the repository to use for server synchronisation, otherwise "master" will be used
mhk user properties soure-server set mhk.git.branch master
```

## To setup a replica (all commands)

```bash
#change
USER=myuser; DB=mydb;  SOURCES=mysources

mhk user properties $USER set mhk.import.auto yes-with-warnings; \
mhk user properties $USER set mhk.import.auto.delay 120; \
mhk user properties $USER set mhk.git.pull.auto yes; \
mhk user properties $USER set mhk.git.pull.auto.delay 10; \
mhk user properties $USER set mhk.import.pull.before yes; \
mhk user properties $USER set mhk.admin $USER; \
mhk user properties $USER set mhk.import.authority.backup yes
```
If you want to have automatic synchronization of identification files do

```bash
mhk user properties $USER set mhk.import.authority.backup yes
```
