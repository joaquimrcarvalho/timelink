# Share you existing Kleio files with git

If you have an existing Kleio installation and want to share the files with git, you can do it by creating a new git repository in the directory containing the Kleio files.

Alternatively you can create a new repository with standard structure and
copy your existing files to it (see [this](new_source_repository_from_template.md))

1. Install VSCode, Git and the Timelink extension. See [this info](install_vscode_git.md).
2. In VSCode open the directory containing your Kleio files.
3. Select the "Source Control" icon in the left menu.
4. You should see a message saying "The folder currently open doesn't have 
   a git repository". Click on the "Initialize Repository" button.
5. A list of the files in the folder will appear under the "Changes" section.
   Click on the "Stage All Changes" button (+).
6. Type a commit message in the "Message" box (e.g. "First commit") and click on the "Commit" button.
7. Click on the "Publish Branch" button.

To share you repository with others you need to register them as collaborators in the repository. See [this info](https://docs.github.com/en/github/setting-up-and-managing-your-github-user-account/inviting-collaborators-to-a-personal-repository).
