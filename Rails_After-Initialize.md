# Rails: After initialize

```ruby
# model.rb
  
  attr_accessor :icon
  after_initialize :init

  def init
    case self.name.downcase
    when 'emails'
      cat_icon = ['far','envelope']
    when 'content'
      cat_icon = ['fas','align-left']
    when 'tips'
      cat_icon = ['far','lightbulb']
    when 'social media'
      cat_icon = ['fas','mobile']
    when 'websites'
      cat_icon = ['fas','desktop']
    when 'landing pages'
      cat_icon = ['far','file']
    when 'design'
      cat_icon = ['fas','paint-brush']
    else
      cat_icon = ['fas','user']
    end

    self.icon ||= cat_icon
  end
```
