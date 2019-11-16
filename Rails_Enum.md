# Rails: enum

## Define Enum
```ruby
# model.rb
enum role: [:user, :vip, :admin, :developer, :marketing, :support, :translator]
```

## Select Input field

```erb
<%# view.rb %>
<%= f.select(:role, User.roles.keys.map {|role| [role.titleize,role]}) %>
```
