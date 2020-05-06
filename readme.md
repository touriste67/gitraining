# Version Management with GIT

TODO:
[ ] develop git config (system, global, local)
[ ] illustrate git staging area (2 files, modify files...)
[ ] play with gitignore add a file exculde by git ignore
[ ] use git status for illustrate the command
[ ] also show in vscode / tree 


## Prerequisite
You need to have git already installed. Open a terminal and type:
```
git
```
On Windows, check if you have GIT BASH already installed > https://confluence.devnet.klm.com/x/a6EfBw

## Configure GIT on your workstation

```
git config --global user.name "Doe, John (DI NB IC) - AF"
git config --global user.email "jodoe@airfrance.fr"
```



## Clone the repository

```
git clone https://bitbucket.devnet.klm.com/scm/gitraining/gittraining.git
```

## Check your status
Use [git status](https://git-scm.com/docs/git-status) command:
```
git status
```

## Create and add to GIT a file locally


1. Create a markdown file (replace below jodoe by your email prefix before the @):
```bash
echo '### John Doe' > jodoe.md
```
2. Add the file > [git add](https://git-scm.com/docs/git-add):
```bash
git add jodoe.md
# or to add all new files
git add -all
```
3. Commit the file > [git commit](https://git-scm.com/docs/git-commit):
```bash
# commit with comment
git commit -m "create new jodoe.md file"
```

### Push the file
