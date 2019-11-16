# Regex

## Getting values between X
#### Example gets value between two quotation-marks

```ruby
"(.*?)"
```

#### Example gets value between two square brackets

```ruby
a = "This is such a great day [cool awesome]"
a[/\[(.*?)\]/, 1]
# => "cool awesome"
a[/(?<=\[).*?(?=\])/]
# => "cool awesome"
```
