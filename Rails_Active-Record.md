# Rails: Active Record

## Create

```ruby
@new_course = Course.new
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

## Find

#### Return only ids

```ruby
@course_lessons   = Lesson.where(:course => @course.id).ids
```

#### Where fields equal X

```ruby
@course_progress  = StepProgress.where(user: current_user.id, :step => @course_steps, :is_completed => 1)
```
