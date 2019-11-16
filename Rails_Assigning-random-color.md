Rails: Assigning Custom Color

```ruby
# model.rb
def color
  colors = %w(#B8BDBF #7080D4 #79C4E5 #00BE89 #FF423D #FB8049 #F3B11C #F36F8F #945ECF #8F9FA5 #61B424 #55A3D9)
  return colors[self.id % colors.count]
end
```
