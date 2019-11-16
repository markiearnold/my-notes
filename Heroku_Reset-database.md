# How to reset PG Database on Heroku?

## Step 1:
```bash
heroku restart
```

## Step 2:
```bash
heroku pg:reset DATABASE
# no need to change DATABASE
```

## Step 3:
```bash
heroku run rake db:migrate
```

## Step 4:
```bash
# if you have seed
heroku run rake db:seed
```
## One liner
```bash
heroku restart; heroku pg:reset DATABASE —confirm APP-NAME; heroku run rake db:migrate
```

Heroku doesn’t allow users from using `rake db:reset`, `rake db:drop` & `rake db:create` command. 
They only allow heroku `pg:reset` and `rake db:migrate` commands.

More info: [https://devcenter.heroku.com/articles/rake](https://devcenter.heroku.com/articles/rake)

If you have more than 1 remote, append—remote [your_remote_name] like this:

```bash
heroku run rake db:migrate —remote dev
# dev is example remote here
```
