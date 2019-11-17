# Rails: Active Record

## Find

#### Return only ids

```ruby
@course_lessons   = Lesson.where(:course => @course.id).ids
```
