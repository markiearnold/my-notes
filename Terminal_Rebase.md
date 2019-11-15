# Terminal: Rebase

To rebase my current branch with `master` branch, follow these steps:

## Basic Commands

```bash
$ git checkout master
$ git pull
$ git checkout my-branch-name
$ git rebase master
$ git push --force-with-lease
```

## Merge Conflicts

* In terminal, when rebasing, it will show any conflicts with the file name and line number.
* Find those files and correct the conflicts.
* After all conflicts have been fixed, run the command below:

```bash
$ git add -A
$ git rebase --continue
```

* If you have no other conflicts throughout rebasing, just run the final command from above:

```bash
$ git push --force-with-lease
```
