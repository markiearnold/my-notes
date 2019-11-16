# Heroku: Commands

## Create

```bash
$ heroku create
> Creating app... done, ⬢ thawing-inlet-61413
> https://thawing-inlet-61413.herokuapp.com/ | https://git.heroku.com/thawing-inlet-61413.git
```

```bash
git remote -v
> heroku  https://git.heroku.com/thawing-inlet-61413.git (fetch)
> heroku  https://git.heroku.com/thawing-inlet-61413.git (push)
```

## Deploy

#### Deploy master

```bash
$ git push heroku master
> Initializing repository, done.
> updating 'refs/heads/master'
> ...
```

#### Deploy a branch

```bash
$ git push heroku testbranch:master
```

## Logs

```bash
$ heroku logs
```

## Open Heroku Site

```bash
$ heroku open
```
