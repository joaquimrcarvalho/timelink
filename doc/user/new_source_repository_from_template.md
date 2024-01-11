# Create a new sources repository with a standard template

To ensure portability of code between `timelink` projects a standard
layout for the directory containing the project `kleio` sources was
created.

## 1. Register in github
To create a new git repository for a new project you 
need first to register or login  with `github` at http://github.com.

## 2. Create a repository
Then go to https://github.com/joaquimrcarvalho/timelink-sources-template 
and click the `Use this template` green button. 

Choose a name for the project repository, decide if it is public or private,  and click on `Create repository from template`. 

It is not
necessary to select the `Include all branches` option.

## 3. Generate a _personal access token_  

If you choose to create a private repository, or if you plan to push back updates,  you will need to
generate a _personal access token_ for MHK to access the repository.

Follow these [instructions](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) on how to generate the _personal access token_.  The simplest form is to generate a "classic" token with the `repo` scope. See https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-personal-access-token-classic 

The token will be used by `Timelink/MHK` to access the repository. It is important to keep it secret.

## 4. Create a timelink/MHK user

If you have a local Timelink/MHK installation, you should create a `timelink` user
to process the data and create a database from the information in the repository.

To create a `timelink` user connected to the new repository follow 
[these instructions](new_user_sources_in_git.md).

For more information see https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template

