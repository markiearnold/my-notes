# Rails: enum

## Define Enum
```diff
- Make sure that name defined in model is same as database column
```
```ruby
# model.rb
enum role: [:user, :vip, :admin, :developer, :marketing, :support, :translator]
```

## Select Input field

```erb
<%# view.rb %>
<%= f.select(:role, User.roles.keys.map {|role| [role.titleize,role]}) %>
```

---

## Integer type

```bash
bin/rails generate Work nickname:string sex:integer
```

Then add a call to enum in the generated model file:

```ruby
class Work < ActiveRecord::Base
  enum sex: [ :male, :female ]
end
```

## View Value

```bash
$ Phone.first.phone_number_type
> "fax"
```

## Change Value

```bash
$ phone.phone_number_type = 1; phone.phone_number_type
> "office"
$ phone.phone_number_type = "mobile"; phone.phone_number_type
> "mobile"
```

Or using bang method:

```bash
$ phone.office!
> true
$ phone.phone_number_type
> "office"
```

## Check Value

```bash
$ phone.office?
> true
```

## Find

```bash
$ Phone.office
> Phone Load (0.3ms)  SELECT "phones".* FROM "phones" WHERE "phones"."phone_number_type" = ?  [["phone_number_type", 1]]
```

If you want to see all the different values you can use, along with the numbers they’re associated with, use the phone_number_types class method:

```bash
$ Phone.phone_number_types
> {"home"=>0, "office"=>1, "mobile"=>2, "fax"=>3}
```
Which makes them easy to put into an HTML form:

```erb
<%# app/views/phones/_form.html.erb %>

<div class="field">
  <%= f.label :phone_number_type %><br>
  <%= f.select :phone_number_type, Phone.phone_number_types.keys %>
</div>
```

## Form
Form not saving as integer, try the following:

```erb
<%= f.select(:role, User.roles.map {|key, role| [key.titleize, role]}) %>
```
