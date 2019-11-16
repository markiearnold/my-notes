## View Repository URL

```bash
$ git remote -v
> origin	git@github.com:USERNAME/REPOSITORY.git (fetch)
> origin	git@github.com:USERNAME/REPOSITORY.git (push)
```

## Start Repository

#### Add local project to existing empty repo

```bash
$ git init
$ git add README.md
$ git commit -m "first commit"
$ git remote add origin git@github.com:USERNAME/REPOSITORY.git
$ git push -u origin master
```

#### Set Git Remote 

```bash
$ git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```
