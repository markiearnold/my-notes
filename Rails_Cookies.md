# Rails: Cookies

## You can set and delete cookies as shown below:
```ruby
cookies[:key] = {
       :value => 'a yummy cookie',
       :expires => 1.year.from_now,
       :domain => 'domain.com'
     }

     cookies.delete(:key, :domain => 'domain.com')
```

```ruby
cookies[:user_name] = "david"
```
