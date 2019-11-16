## Terminal: GIT Cheatsheet

## Overview

    $ g remote add origin https://darllxd@github.com/ueccssrnd/name-of-project.git
    $ g remote set-url origin git://new.url.here
    Check last 2 diffs: g log -p -2 
    

    Cancel last commit: git reset --soft HEAD~1. Then you can do a gre (git reset --hard HEAD && git clean -f) after. So this "cancels a commit".

#### You pushed a wrong commit message.

    $ git reset --soft head~
    $ git commit -m "new commit message"
    $ git push -f

#### Branches

> View remote

    $ git branch -r

> View all

    $ g branch -a

> Check last commit of each branch

    $ git branch -v

> Pull from remote the branch `fix_stuff`

    $ g checkout -b fix_stuff origin/fix_stuff

#### Deleting

    $ g branch -d local_branch_to_be_deleted
    
    # $ g push [REMOTE] :[NAME_OF_REMOTE_BRANCH]
    $ g push origin :facebook_integration

> Pull from remote but different branch

    $ g pull [remote_location] [remote_branch]
    $ g pull origin master

> Cloning from BB

    $ g clone https://daryllxd@bitbucket.org/icanpassaccounting/icpa.git icpa_redesign

---

## Amend
Amend a commit. Add more changes to the last commit. Change commit message.

```bash
$ git commit --amend 
$ git commit --amend -m “message”
```

## Diff
Check changes since last commit

```bash
$ git diff
$ git diff --staged //difference from the staged(git add) files
```

## Log
Git log. (Check commit history)

```bash
$ git log
$ git log -n <limit> //limit
$ git log --oneline //Condense
$ git log --stat //stats
$ git log --author="<pattern>" //commits from specific author
$ git log <file> //commits including a file
$ git log --graph --decorate --oneline
```

## Blame
Blame (check all detailed changes in a file)

```bash
$ git blame <FILE>
$ git blame <FILE> --date short
```

## Remove

```bash
$ git rm <FILE> //removes file
$ git rm '*.txt' //remove all files with extension .txt
```

## Remove all changes since last commit to the file.

```bash
$ git checkout -- <FILE>
$ git reset HEAD <FILE>
```

## Untrack
Make a file untracked. Remove file from git index. But keep the file:

```bash
$ git rm — cached <FILE> //make the file untracked
```

## Undo
Resetting the Stage. (Unstage)

```bash
$ git reset <FILE>
```

## Stash
Put our work to a stack until we pull new changes from remote.

```bash
$ git stash //stash unstaged changes  
$ git stash save "add style to our site" //stash with a message
//pull from remote and merge
$ git stash show //show stash 
$ git stash show -p //show the diff of stash
$ git stash list
$ git stash pop 
OR 
$ git stash pop stash@{0} //stash@{0} - stash number
$ git stash apply
```

## Tagging

```bash
$ git tag //list tags
$ git checkout <TAG> //checkout the code at tag(version)
$ git tag -a v0.0.3 -m "version 0.0.3" //create a new tag v0.0.3
$ git push --tags
```

## ALIASES-DESU for add + commit

    $ g config --global alias.add-commit '!g add -A && g commit'

## ALIASES-DESU for last

    $ g config --global alias.last ’log -1 HEAD’
