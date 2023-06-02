# Install VSCode and Git for Timelink data entry

To be able to enter data in Timelink, you need to install VSCode and Git,
as well as the Timelink extension for VSCode.

## Install VSCode

1. Download and install VSCode from [https://code.visualstudio.com/](https://code.visualstudio.com/)


## Install Git

1. Download and install Git from [https://git-scm.com/downloads](https://git-scm.com/downloads)

## Create an account in GitHub

1. Create an account in [GitHub](http://github.com)    
## Install the GitHub Pull Requests and Issues extension for VSCode

1. Open VSCode
2. Click on the Extensions icon in the left menu
3. Search for "GitHub Pull Requests and Issues"
4. Select GitHub Pull Requests and Issues
5. Click on the Install button

## Configure Git in VSCode

Git needs your name and email to be able to commit changes to the repository,
so that others know who made the changes.

Git also needs to know how to merge changes from the repository with your
local changes. There are two alternatives: merge or rebase. The recommended
strategy is rebase, so that is what we will configure. To know more about
the difference between merge and rebase, see [this article](https://sdq.kastel.kit.edu/wiki/Git_pull_--rebase_vs._--merge)

1. Open VSCode (quit and restart if it was already open)
2. Open a terminal window (View -> Terminal)
3. Type the following commands in the terminal window:
   ```
   git config --global user.name "Your Name"
   git config --global user.email "Your email"
   git config --global pull.rebase true
   ```
4. Close the terminal window
    
## Install the Timelink extension for VSCode

1. Open VSCode
2. Click on the Extensions icon in the left menu
3. Search for "Timelink"
4. Select Time Link Bundle (Web version)
5. Click the "Reload" button to reload VSCode
   

## Create a Timelink source repository or clone and existing one

To create Timelink files with VSCode, you need to create a Timelink source repository, or clone an existing one.

### To create a new Timelink source repository

For new projects create a Timelink source repository from the [Timelink sources template](https://github.com/joaquimrcarvalho/timelink-sources-template).

1. Login in Github.com
2. Then go to https://github.com/joaquimrcarvalho/timelink-sources-template 
3. Click the `Use this template` button. 
4. Choose a name for the project repository, decide if it is public or private,  and click on `Create repository from template`. It is not
necessary to select the `Include all branches` option.

### To clone an existing Timelink source repository

You need the URL of the repository to clone it. This will be provided
by the project manager. Also, if you are contributing to the existing
repository, you will need to be added as a collaborator by the project
manager.

1. Login in Github.com
2. Go to the repository page (get the URL from the project manager)
3. Click on the `Code` button
4. Copy the URL of the repository
5. Open VSCode
6. Click on the `Clone Repository` button
7. Paste the URL of the repository
8. Choose a folder to store the repository
9. Click on the `Clone` button
    

