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

## Enum integer type

```bash
bin/rails generate Work nickname:string sex:integer
```

Then add a call to enum in the generated model file:

```ruby
class Work < ActiveRecord::Base
  enum sex: [ :male, :female ]
end
```
