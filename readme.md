
# Version Management with Git

## Prerequisite

### Git BASH
You need to have git already installed. Open a terminal and type:
```
git
```
On Windows, check if you have Git BASH already installed > https://confluence.devnet.klm.com/x/a6EfBw

### VSCode IDE
You need Visual Studio Code and some plugins:
1. Go to https://code.visualstudio.com/ to download and then install VSCode.
2. Add https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph extension.


> By default VSCode has an embedded Git Client and a lot of extensions for Git exist.


### Markdown
[Markdown](https://fr.wikipedia.org/wiki/Markdown) files will be used for the exercises ([Play with markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)).

---

## Initialization

### Configure Git on your workstation. 

```
git config --global user.name "Doe, John (DI NB IC) - AF"
git config --global user.email "jodoe@airfrance.fr"
```

### Understand Git config
Git config allows to configure git with your settings. There are 3 levels of configuration: local, global and system. The local config overwrites the global config which overwrites the system config.

> To modify your configuration you can use the git config command [git config](https://git-scm.com/docs/git-config) or [edit the configuration file for each level](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup).

#### List all variables

Your configuration:
```
git config -l
```

Same for each levels:
```
git config --local -l
git config --global -l
git config --system -l
```

### Edit the config files

Edit the config file and locate them on your workstation
```
git config --local --edit
git config --global --edit
git config --system --edit
```

#### Overwrite a system variable

```bash
# visualize the variable
git config --get-all core.quotepath
git config --get core.quotepath

# set the variable
git config --global core.quotepath true

# visualize the variable again
git config --get-all core.quotepath
git config --get core.quotepath

# unset the variable
git config --global --unset core.quotepath
```

#### Add alias to config

A Git alias is a shortcut to a command.

Examples of useful aliases:

```bash
git config --global alias.l log --graph --all --pretty=format:'%C(yellow)%h%C(cyan)%d%Creset %s %C(white)- %an, %ar%Creset'
# Usage
git l

git config --global alias.lg log --color --graph --pretty=format:'%C(bold white)%h%Creset -%C(bold green)%d%Creset %s %C(bold green)(%cr)%Creset %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative
# Usage
git lg

git config --global alias.ll log --stat --abbrev-commit
# Usage
git ll

git config --global alias.llg log --color --graph --pretty=format:'%C(bold white)%H %d%Creset%n%s%n%+b%C(bold blue)%an <%ae>%Creset %C(bold green)%cr (%ci)' --abbrev-commit
# Usage
git llg

```

---

## Git basics

### Clone the repository
Use [git clone](https://git-scm.com/docs/git-clone) command by default a directory named as the repository name is created and contained the local repository:
```bash
# create an empty directory (named for example git) on your workstation
mkdir git
cd git/
# clone the repository
git clone https://bitbucket.devnet.klm.com/scm/gitraining/git-training.git
# navigate in the local git repository
cd git-training/
```

> ***TIP***: Specify the destination directory with git clone
> ```bash
> # The destination directory is toto
> git clone https://bitbucket.devnet.klm.com/scm/gitraining/git-training.git toto
> ```
> ---

### Check your status
Use [git status](https://git-scm.com/docs/git-status) command:
```bash
git status
```

### Manipulate a file locally

The schema below illustrates the manipulation that will be done ([more details](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)):

![logo](https://git-scm.com/book/en/v2/images/lifecycle.png)

#### 1. Ignore file and clean untracked file

> Commands needed:
> - [git status](https://git-scm.com/docs/git-status)
> - [git clean](https://git-scm.com/docs/git-clean)

```bash
# check the status
git status
# create a markdown file (replace below jodoe by your email prefix before the @)
echo 'empty' > ignore_me.txt
# check the status, nothing change (file is ignore)
git status
# see the gitignore file
cat .gitignore
# rename the file
echo 'empty' > not_ignore_me.txt
# check the status, file is not ignored anymore
git status
# clean untracked file / remove the file and directories
git clean -fd 
ls -al
```

> ***MORE***: You can edit and remove the ignore_me.txt file

#### 2. Create and add a file locally

> Commands needed:
> - [git add](https://git-scm.com/docs/git-add)
> - [git commit](https://git-scm.com/docs/git-commit)

```bash
# create a markdown file (replace below jodoe by your email prefix before the @)
echo '### John Doe' > jodoe.md
# check the status
git status

# add the file to staged
git add jodoe.md
# check the status
git status

# commit with comment
git commit -m "create new jodoe.md file"
# check the status
git status
```

> ***TIP***: Add all untracked files
> ```bash
> git add --all
> ```
> ---

#### 3. Modify the file a file locally

```bash
# modify/edit the file
echo 'is an unknown man' >> jodoe.md
# check the status
git status
# add the modification of the file to staged
git add jodoe.md

# commit with comment
git commit -m "modify jodoe.md file"
# check the status
git status
```

#### 4. Consult the history 

> Commands needed:
> - [git log](https://git-scm.com/docs/git-log)
> - [git show](https://git-scm.com/docs/git-show)
> - [git diff](https://git-scm.com/docs/git-diff)

```bash

# consult history
git log
git show

# comparison between local (staged and workspace) and HEAD 
# !!! TODO > git diff mixed do not exist use so git status -vv !!!
git status -vv
echo 'more info about jodoe' >> jodoe.md 
git status -vv
git add jodoe.md
git status -vv

# show commits 
git log --oneline

# comparison between workspace and a commit (get with the command above)
git diff <commit1>
git diff <commit2>

# comparison between two commits (use commit above)
git diff <commit1> <commit2>
```

#### 5. Reset modification of a file

> Command needed:
> - [git checkout](https://git-scm.com/docs/git-checkout)

```bash
git status
git checkout master jodoe.md
git status
```

#### 6. Untrack the file

> Command needed:
> - [git rm](https://git-scm.com/docs/git-rm)

```bash
# untrack the file
git rm --cached jodoe.md
# check the status
git status

# commit with comment
git commit -m "untrack jodoe.md file"
# check the status
git status

# track again the file
git add jodoe.md
git commit -m "jodoe.md file is back"
```

#### 7. Remove the file

```bash
# untrack the file
git rm jodoe.md
# check the status
git status

# commit with comment
git commit -m "delete jodoe.md file"
# check the status
git status
```

> ***TIP***: Delete the file is the same as the ***git rm*** command
> ```bash
> rm jodoe.md
> ```
> ---


#### 8. Stash and amend commit

1. Save the file (stash)

```bash
# create a new file
echo one > jodoe_one.txt
# do not commit, save for later (-u for include untracked files)
git stash -u
# the file is not present anymore
ls -al
# list stash
git stash list
```

> ***TIP***: Name the stash has 'toto'
> ```bash
> git stash save -u toto
> ```
> ---


2. Amend commit (stash)

```bash
# watch the current commits
git log --oneline
git show
# create a new file
echo 'amend file' > jodoe_amend.txt
git add jodoe_amend.txt
# add the file to the command without modifying the commit message (--no-edit)
git commit --amend --no-edit
# watch the current commits
git log --oneline
git show
```

> When you amend a commit the id of the commit change.

3. Get what you saved

```bash
git stash pop
ls -al
```

#### 9. Reset and clean

1. Reset all your commits

Reset commits and go back to the reference origin/master
```bash
git log --oneline

# Reset all
git reset --hard origin/master
# Finish the cleaning
git clean -fd

ls -al

git log --oneline
```

2. Restore the commits

You've made a mistake, you want to restore the commits. For that you have reset by using the reference ORIG_HEAD.

```bash
git reset --hard ORIG_HEAD
git log --oneline
```

3. Remove last commit

```bash
# reset last commit
git reset --soft head^
# check the files
git status
```

4. Squash all in one commit

```bash
git log --oneline

# reset all commits from reference origin/master
git reset --mixed origin/master
# check the files
git status

git add --all
git commit -m "result of squashed commits"

git log --oneline
```

5. Add a tag

> Command needed:
> - [git tag](https://git-scm.com/docs/git-tag)

```bash
git log --oneline
git tag v1.0 master
# check that the tag was added
git log --oneline
```

6. Clean all before working in team
```bash
git log --oneline

git reset --hard origin/master

git log --oneline
# in addition you can check the diff between master and v1.0
git diff master..v1.0
```

---

## Work in team


<a name="update-your-local-repository-with-remote-repository-data"></a>

### 1. Update your local repository with remote repository data

> **Wait for trainer instructions before continuing the exercises.**
>
> To do by trainer only:
> <details>
>
> Commit a file on the main branch, then ask trainees to fetch
>
> ```bash
> echo 'from the trainer' > trainer.txt
> git add trainer.txt
> git commit -m 'add trainer.txt'
> git push origin master
> ```
>
> </details>

> Commands needed:
> - [git fetch](https://git-scm.com/docs/git-fetch)
> - [git merge](https://git-scm.com/docs/git-fetch)

```bash
# check the difference between your master branch and the origin/master
git diff origin/master
git log --oneline

# fetch the modification from the remote repository and update your local repository
git fetch

# check again to see the modifications
git diff origin/master
git log --oneline

# merge the modifications
git merge origin/master
git log --oneline
```

### 2. Update your current branch with a commit from the tag v1.0

> Command needed:
> - [git cherry-pick](https://git-scm.com/docs/git-cherry-pick)

```bash
# check the difference
git diff v1.0
git log --oneline

# pick this commit to update master
git cherry-pick v1.0

# check the difference
git diff v1.0
git log --oneline
```

### 3. Synchronize your work with others trainees

> Command needed:
> - [git pull](https://git-scm.com/docs/git-pull)

> **Wait for trainer instructions before continuing the exercises.**
>
> To do by trainer only:
> <details>
>
> Commit a file on the main branch, then ask trainees to fetch
>
> ```bash
> echo 'another line!!!' >> trainer.txt
> git add trainer.txt
> git commit -m 'add another line in trainer.txt'
> git push origin master
> ```
>
> </details>

```bash
# try to push your work on the remote repository
git push origin master
```

> ***TIP***:
> ```bash
> git push origin master
> # or simply if you already have done it.
> git push
> ```
> ---

To solve a rejected push, you have to resynchronized your local repository with the remote like [Update your local repository with remote repository data](#update-your-local-repository-with-remote-repository-data).

```bash
# synchronize
git pull origin master
# and push again
git push origin master
```

> ***TIP***:
> ```bash
> git pull = git fetch + git merge
> ```
> ---

### 4. Synchronize your work with others trainees with conflict

> **Wait for trainer instructions before continuing the exercises.**
>
> To do by trainer only:
> <details>
>
> Create a file with on each line the name of trainees
>
> ```bash
> echo 'trainee1' > trainees.txt
> echo 'trainee2' >> trainees.txt
> echo 'trainee3' >> trainees.txt
> echo 'trainee4' >> trainees.txt
> git add trainees.txt
> git commit -m 'add trainees.txt'
> git push origin master
> ```
>
> </details>

```bash
# Retrieve the trainees.txt file from the remote
git pull origin master

# Modify the line with your name by adding something at the end
vim trainees.txt
# Add something

git add trainees.txt
git commit -m 'trainee x add something'
```

> **Wait for trainer instructions before continuing the exercises.**
>
> To do by trainer only:
> <details>
>
> Modify each line of trainees file
>
> ```bash
> echo 'aaa trainee1' > trainees.txt
> echo 'aaa trainee2' >> trainees.txt
> echo 'aaa trainee3' >> trainees.txt
> echo 'aaa trainee4' >> trainees.txt
> git add trainees.txt
> git commit -m 'modify trainees.txt'
> git push origin master
> ```
>
> </details>

```bash
# Retrieve the trainees.txt file from the remote
git pull origin master
# Check the file in conflict
git status
git diff
```

> You have a **CONFLICT**

> ***TIP***: In a file with conflicts, there's some information added by git to show you a conflict like in the example below:
> ```bash
> ++<<<<<<< HEAD
> +man1!
> ++=======
> + yoman1
> ++>>>>>>> e3def26848fb883b4f775529ca83e1a7c1fa8444
> ```
> ---

### 5. Resolve a conflict

```bash
# Edit the file in conflict
vim trainees.txt
# Suppress what you don't need and keep what you need.

# Mark the conflict resolved
git add trainees.txt

git commit -m 'conflict resolved'

# Do several time the actions below to get the modification of other trainees.
git push origin master
git pull origin master
```


---

**TODO**

git merge --ours


TEST videos

[![](http://img.youtube.com/vi/CRlGDDprdOQ/0.jpg)](http://www.youtube.com/watch?v=CRlGDDprdOQ "")