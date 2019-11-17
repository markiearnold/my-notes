# Rails: Active Record

## Find

#### Return only ids

```ruby
@course_lessons   = Lesson.where(:course => @course.id).ids
```

#### Where fields equal X

```ruby
@course_progress  = StepProgress.where(user: current_user.id, :step => @course_steps, :is_completed => 1)
```
