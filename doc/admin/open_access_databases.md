# How to open access a database

To open access a database it is necessary
to create a "guest user" with access level 1.

This user will use the same database
as a level 3 user and the same sources.

Replace guestuser, opendb and mysources with the relevant values in your case:

    USER=guestuser; DB=opendb;  SOURCEDIR=mysources

    mhk user create $USER  --database $DB --level 1 --sources $SOURCEDIR

Enable access by captcha in MHK login
screen. This allows users to login
with no password

    mhk user properties $USER set mhk.login.captcha yes

Additionally it is possible to generate
a URL for direct access to the database

This needs a token that acts as password:

    mhk user token $USER

    ...

    Login token for guestuser

        Zepvzt.....

    Use with utoken param on requests.

