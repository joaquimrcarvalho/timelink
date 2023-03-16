# Using submodules 

It is possible to use submodules to create a Timelink 
instalation which aggregates several source repositories.

Submodules are a technique in git that allows for 
including links to other repositories in a given repository.

## Cloning a repository with submodules

With mhk do

```bash
mhk sources clone URL TOKEN DIR --recurse-submodules 
   ```

Currently the automatic repository refresh of MHK does not
update the submodules versions.

In a terminal in the sources directory of the project do:

```bash
git submodule update --remote --merge
```
> from https://stackoverflow.com/questions/5828324/update-git-submodule-to-latest-commit-on-origin
