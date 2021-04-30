# Tags in docker images

## Tag types 

We follow the advice of https://docs.microsoft.com/en-us/azure/container-registry/container-registry-image-tag-version

Each of Kleio-server, mhk-tomcat and mhk-manager images can receive 3 types of tags

`Latest`  (Tag: latest) is the last build that will be used by default to update and run all services.
`Stable` (Tag: $Version-$minor-version)  is the last stable build of a specific version.
`Unique` (Tag: $current-build-number)  is a specific build

## Ant Targets

### Building images

There are three Ant targets to build the images

    docker-build-kleio
    docker-build-manager
    docker-build-tomcat

They create images tagged with the build number and also untagged images, which receive by default the `latest` tag in the local machine.

Each of this targets increments the build number.

### Ant targets for tagging

Various build targets create images with no tags and with _unique_ tags for the current build number and _stable_ images for specific versions.

Note that images with no tags have the assumed tag “latest” in the local machine.

The targets

    docker-tag-unique
    docker-tag-stable

are used to tag the three images with the latest build number and the current version.

Since each build increments the global build number the images of the different services will end up with different unique tags. The target `docker-tag-unique` ensures that all current images of services receive the tag corresponding to the last build numbers.

### Ant targets to push images to Docker hub

The target 

	docker-push-latest

 tags the most recent images with no tags with the tag `latest` and pushes them to docker hub. Use this to allow mhk instalations to update to the latest version.

 	docker-push-stable

Pushes the images with the tag `$version-minor-version` currently on the local machine. The version numbers are the current ones in the build.xml file. Use this if for some reason you need to update installations that want to remain in a previous version. Note that those installations must have been set up to update from a specific version, and not from latest

	docker-push-unique

Push the current build.  Use this to test a development build in another machine without disturbing the latest version and stable versions. On the remote machine you need set mhk to update from a specific build number.


## How to use in mhk update

By default mhk update uses the latest images for updates

But you can make mhk update a specific tag using the command

        mhk use-tag TAG

Followed by

        mhk update

If you have different images with different tags in a machine you can also run mhk from different images with

        mhk use-tag TAG
        mhk start

## Development workflow

On the development machine ensure mhk use-tag latest


    mhk use-tag latest

Use build targets to create new images and update  with

	mhk update —local 

Run and test


If all services pass QA then use the following targets to publish the update to other machines

	docker-push-latest
	docker-push-stable

## Details

The docker compose file used to run and "pull" the images from the repository used the tag in the environment variable `TAG`.

The current value for the variable is stored in file `mhk-home/app/.env`.

The command `mhk use-tag` sets the value of `TAG`in the file.

If the variable is not set at the time execution of the commands `start`, `up` and `update`. the manager sets it to `latest`.



