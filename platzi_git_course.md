# Git commands

## User configuration

Git looks up different files for the different configuration scopes. Most important scopes are: ``local`` (which is configuration for the current repo), ``global`` (which is for the current user) and ``system`` (which is cross-user configuration).

To access the different settings, a section followed by a dot, and a key have to be provided, i.e, ``git config user.name``.

To provide a scope, then double dashes (--) followed by the scope name must be provided as an argument to ``git config``, i.e, ``git config --global user.name``

To see where the different files for the different scopes and the settings are located, ``git config --list --show-origin`` must be used. The results can be as follows:

    (...)
    file:C:/Program Files/Git/etc/gitconfig  init.defaultbranch=master
    (...)
    file:C:/Users/aspiringdsc/.gitconfig  user.name=aspiringDataSc
    (...)
    file:.git/config  core.ignorecase=true

_some results were hidden for security reasons._

As one can see, ``C:/Program Files/Git/etc/gitconfig`` is where the system settings are. ``C:/Users/aspiringdsc/.gitconfig`` is for global settings and ``.git/config`` is for the current repo's.

## Git workflow areas

Git uses three main areas our files can be in that serve different purposes:

1. Working directory: This is where all the untracked/modified files are in.

2. Staging: where files that want to be tracked are included. It's an area that comes before submitting changes to the actual repo. To add files to this area, ``git add <filename>`` must be used.

3. Repository: when ``git commit -m <message>`` is used, changes are applied to the actual repository branch we are working on.

4. Remote repository: After all the changes want to be exported to the online external respository, then they can be pushed using ``git push origin <branch>``

<img src="https://snipcademy.com/img/articles/git-fundamentals/three-stages-01.svg" alt="process example">

### Undo changes

It's important to know how to undo unwanted changes. To go back to a commit, one can do:

* ``git reset --soft <commit SHA>`` this will go back to the commit and delete all the newer commits from that moment on.

* ``git reset --mixed <commit SHA>`` this will do the same thing as the previous reset, but the commit included will be in the working directory. (changes won't be applied but the commits after the one we specified will be deleted)

* ``git reset --hard`` it deletes everything.

* ``git reflog`` will show all the commit history even if the commits were deleted. It should be used before ``git reset --hard <deleted commit SHA>`` to revive a deleted commit.

## Commit history and logs

To have more information about the changes done, one can output various things.

``git log`` shows the commit history for the branch we are in. To make this a little bit more summarized, one can use ``git log --oneline``.

``git log`` shows where the current ``HEAD`` is (or the last commit of the project) is. This is important to check the differences between the different branches.

Another tool git provides is ``git diff <commit A hash> <commit B hash>`` which helps compare two commits to see what differs.

Also, ``git show <filename>`` shows the latest changes made to a file.

## Branches

Git uses branches as a way to facilitate collaborative work. Also, to help making changes to a project without actually modifying what's in production.

One can think of branches as development lines where features are being worked on. Their lifecycle always ends in merging with the master (or main) branch so that changes are applied.

To create a new branch and switch to it, one can do ``git checkout -b <branch_name>``.

To list all branches in the project, ``git branch`` will do the job.

## Remote repositories

To set a remote repo, one has to tell git where the repo is located, and that's done with ``git remote add origin <github_link>``. Then, our current local branch has no remote tracking branch (which is just fancy argo for the remote branch our local branch is liked to), to set it, do ``git remote add origin git@github.com:edseldim/git_notes.git`` and ``git push origin HEAD:<branch_name>``


Now, all the changes can be sent to the external repo using ``git push origin``.

To update our local repo with the external repo's changes, do ``git pull origin`` (**This is recommended to do before we want to modify something in the branch**)





