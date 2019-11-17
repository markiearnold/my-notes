# Rails: Active Record

## Create

```ruby
@new_user = User.new
```

```ruby
user = User.new
user.name = "David"
user.occupation = "Code Artist"
```

```ruby
user = User.new
user.name = "David"
user.occupation = "Code Artist"
```

```ruby
user = User.new
user.name = "David"
user.occupation = "Code Artist"
```

## Read

```ruby
users = User.all
```

```ruby
# return the first user
user = User.first
```

```ruby
# return the first user named David
david = User.find_by(name: 'David')
```

```ruby
users = User.where(:occupation => @occupation.id).ids
```

```ruby
# find all users named David who are Code Artists and sort by created_at in reverse chronological order
users = User.where(name: 'David', occupation: 'Code Artist').order(created_at: :desc)
```
