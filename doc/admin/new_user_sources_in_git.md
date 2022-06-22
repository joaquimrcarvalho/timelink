# Creating an user with sources in a git repository

This explains how to create a MHK user in a local computer with the sources directory linked from a git repository

First you need to have a git repository for sources files. To create one see DOC creating a new Git repository for Kleio files

# Get the sources from git

## 1. Get the Git information

You will need the URL of the git repository and a Personal access token. See the documentation above on how to create a repository and a Personal access token.

## 2. Determine a name for the sources directory

You must choose a name for the local sources directory.

The directory will be created in the mhk-home/sources/ directory

For instance mysources

## 3. Clone the Repository

 mhk sources clone URL TOKEN DIR

For instance

    mhk sources clone https://github.com/joaquimrcarvalho/soure-fontes.git  336b0.. mysources

    cd ~/mhk-home/sources/mysources

    git log


..........

## 4. Create an user associated with the sources you just cloned

    mhk user create myuser  --database myuser --level 3 --sources mysources

This will ask for a password

5. Restart mhk

    mhk stop
    mhk start

## 5. Optionally set auto import

You can have mhk automatically checking if there are new sources ready for import. This is useful in an installation that is publishing a public
database. 

For an installation used for data entry with the
timelink VSCode extension, auto import can generate many unnecessary
imports. If used set a long delay between checks. 

    mhk user properties myuser set mhk.import.auto yes

Also set a reasonable interval to run the checks, in seconds, for instance every 2 minutes

    mhk user properties myuser set mhk.import.auto.delay 120

## 6. Optionally set git auto pull

If you want to keep your repository synchronised with the remote repository on GitHub or similar you can have mhk to do a periodical auto pull.
> Note this only makes sense if you are sitting up a replica and the sources are being updated by someone else and you just want to keep your local copy in sync.

    mhk user properties myuser set mhk.git.pull.auto yes

You can also set the delay between pulls in minutes

    mhk user properties myuser set mhk.git.pull.auto.delay 5


# Summary

    USER=myuser; DB=mydb;  SOURCES=mysources

    mhk user create $USER  --database $DB --level 3 --sources $SOURCES

## set up a replica with sync of ids

    mhk user properties $USER set mhk.import.auto yes-with-warnings; \
    mhk user properties $USER set mhk.import.auto.delay 120; \
    mhk user properties $USER set mhk.git.pull.auto yes; \
    mhk user properties $USER set mhk.git.pull.auto.delay 10; \
    mhk user properties $USER set mhk.import.pull.before yes; \
    mhk user properties $USER set mhk.admin $USER; \
    mhk user properties $USER set mhk.import.authority.backup yes

If you want to have automatic synchronization of identification files do

mhk user properties $USER set mhk.import.authority.backup yes