# [Rails Sortable](https://github.com/itmammoth/rails_sortable)

## Setup

Add to gemfile
```ruby 
gem 'jquery-rails'
gem 'jquery-ui-rails'
gem 'rails_sortable'
```

Add to application.js
```
//= require jquery
//= require jquery_ujs
//= require jquery-ui/widgets/sortable
//= require rails_sortable
```

## Extending

Rails sortable is using [jQueryUI sortable](https://jqueryui.com/sortable/)

You are able to extend:
```javascript
$(function() {
  $('.sortable').railsSortable();
});
```

The same way you can in jQueryUI
```javascript
$(".sortable").railsSortable({
  update: function( event, ui ) {
    my_custom_function();
  }
});
```

See all [events](http://api.jqueryui.com/sortable/) available.
