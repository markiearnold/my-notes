# Ruby: Integer Formatting

## Examples

```ruby
# Remove leading zeros
str.sub!(/^[0]+/,'')
```

```ruby
# Add leading zeros
puts 1.to_s.rjust(3, “0”)
#=> 001
puts 10.to_s.rjust(3, “0”)
#=> 010
puts 100.to_s.rjust(3, “0”)
#=> 100
```

```ruby
# Round decimal to x places
sprintf('%.2f', number)
```

```ruby
# Round integer to nearest integer
5.44.round
=> 5
5.54.round
=> 6
```

```ruby
# Round integer up
(number.to_f).ceil
```

```ruby
# Round integer down
(number.to_f).floor
```

```ruby
# 1200 to 1.2K
number_to_human(1200, 
	:format => '%n%u', 
	:precision => 2,
	:units => {
		:thousand => 'K',
		:million => 'M', 
		:billion => 'B'
 	})
```

## Resources
* [https://floating-point-gui.de/languages/ruby/](https://floating-point-gui.de/languages/ruby/) 
