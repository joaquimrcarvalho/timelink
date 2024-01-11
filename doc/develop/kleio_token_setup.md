# Kleio-server token setup

MHK needs a special token to access the Kleio server
with privileges to create user tokens. This is
called an administration token.

The token must be shared between the MHK web app
and the Kleio Server running in a different container.



## Getting an admin token

The `MHK manager` (mhk-home/app/manager) shell script sets up
the KLEIO_ADMIN_TOKEN environment variable
before launching the MHK webapp and the
Kleio Server. Since both apps check that
variable on startup communication is ensured.



As of version 5 build 2235 (master) 06/08/2023 04:31
the manager script proceeds as follows:

1. the `manager` checks the configuration file at `mhk-home/system/conf/mhk_system.properties`
   for the property `mhk.kleio.service.token.admin`.
   This is done with:

   ```bash
   KLEIO_ADMIN_TOKEN=$(grep ^mhk.kleio.service.token.admin  "$HOST_MHK_HOME/system/conf/mhk_system.properties" | sed 's/mhk.kleio.service.token.admin=//g')
   ``` 

   if there is no property in the file then MHK
   generates a random token and adds it to
   mhk_system.properties file:

   ```bash
   if [ -z "$KLEIO_ADMIN_TOKEN" ]; then
      echo "No Kleio server token found. Generating one."
      KLEIO_ADMIN_TOKEN=$(openssl rand -hex 32)
      echo "mhk.kleio.service.token.admin"="$KLEIO_ADMIN_TOKEN" >> "$HOST_MHK_HOME/system/conf/mhk_system.properties"
   fi
   ```

2. The variable `KLEIO_ADMIN_TOKEN` is then `exported`
   before the launch of the `MHK` service and both the
   Kleio server and the MHK web app will share the same admin token.

Note that if a specific token needs to be shared it can be
entered in the  `mhk-home/system/conf/mhk_system.properties` file
   as property `mhk.kleio.service.token.admin`.

The manager will use that value and set the `KLEIO_ADMIN_TOKEN` variable
before launching the Kleio Server and the MHK web app.








