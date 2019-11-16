# Custom field on model

```ruby 
class Document < ApplicationRecord
  attr_accessor :page_types
  
  def page_types
    DocumentPage.group(:display).where(document: self).count
  end
end
```

`Document.page_types` returns:
```ruby
[
  {image: 2},
  {video: 4},
  {text: 1}
]
```

---

```ruby 
class Project < ApplicationRecord
  attr_accessor :progress
  
  def progress
    options = Project.phase_options(self.roadmap)
    phase_exists = options.map{|k,v| v}.index(self.phase)
    if !phase_exists.nil?
      "#{phase_exists + 1}/#{options.count}"
    end
  end
end
```

`Project.progress` returns:
```ruby
"2/6"
```
