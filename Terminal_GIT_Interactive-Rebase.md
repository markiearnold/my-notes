# Terminal: GIT Interactive Rebase

```bash
$ git log
$ git rebase -i [sha]

# insert
# change pick to f to put in last (above)
# change pick to r to reword
esc
:wq

# rename commit message
$ git rebase --continue
```
