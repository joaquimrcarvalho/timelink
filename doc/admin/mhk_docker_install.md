# MHK/Timelink manager and installer (experimental)

Installs MHK/Timelink on Linux, Macos and Windows machines, using Docker and provides command line management commands for MHK.

You need to install Docker Desktop on MacOS and Windows, and on Linux using the system package manager.

_This Docker version is work in progress, under tests_

## First time install of MHK

The installer needs be run the first time in an empty directory. 

The directory will become the `mhk-home` where all the MHK related files will be kept.

Most users will create a directory named `mhk-home`in their home directory. If you want to create mhk-home in another location on your computer you must navigate to the desired directory before executing the commands bellow.

### On MacOS ###

First install Docker Desktop from https://www.docker.com/products/docker-desktop.

To create the mhk-home directory in the home directory and install MHK open a terminal window and type:

```bash
mkdir -p mhk-home
cd mhk-home
docker run -v ${PWD}:/mhk-home -it joaquimrcarvalho/mhk-manager mhk-install && sh app/manager init
```

or in a single line:

```bash 
mkdir -p mhk-home && cd mhk-home && docker run -v ${PWD}:/mhk-home -it joaquimrcarvalho/mhk-manager mhk-install && sh app/manager init
```
Close the terminal window and open a new one.

Test if the install was successful with 

```bash
mhk --version
```
### On Windows ###

MHK is tested on Windows 10 with `WSL` (Windows subsystem for linux).

For current documentation on how to install WSL on Windows 10 see https://docs.microsoft.com/en-us/windows/wsl/install

Currently:

1. Install `WSL`:  on windows command prompt or PowerShell type 

```bash
wsl --install
```

Restart windows

2. Setup Linux user info

Check https://docs.microsoft.com/en-us/windows/wsl/setup/environment#set-up-your-linux-user-info

3. Install docker desktop

Goto https://docs.docker.com/docker-for-windows/wsl/#download

4. Enter the `WSL` command window:

Type wsl in the search field of the windows task bar.

On the terminal window type:

```bash
cd 
mkdir -p mhk-home
cd mhk-home
docker run -v ${PWD}:/mhk-home -it joaquimrcarvalho/mhk-manager mhk-install && sh app/manager init
```
After installation type 

```bash
mhk --help
```


5. To see the contents mhk-home in windows file explorer:

Type wsl in the search field of the windows task bar.

On the terminal window type:
```bash
cd
cd mhk-home
explorer.exe .
```

 
### On Linux (tested on CentOs)

Make sure that user running the docker command is part of group docker (`sudo usermod -a -G docker $USER`)

On a terminal window do:

```bash
mkdir -p mhk-home
cd mhk-home
docker run -v ${PWD}:/mhk-home -it  --user "$(id -u):$(id -g)"  joaquimrcarvalho/mhk-manager mhk-install && sh app/manager init
```


Test if the install was successful in a new terminal window :

```bash
mhk --version
```

## Starting and stopping MHK

To start MHK after the install do

```bash
mhk up
```
Point your browser to http://localhost:8080/mhk2019

To stop:

```bash
mhk stop
```

To check if MHK components are running:

```bash
mhk ps
```

For more MHK commands:

```bash
mhk --help
```
