# Rails: After Commit

## After Create

```ruby
# model.rb

  after_create_commit	:create_styleguide

private

  def create_styleguide
    Styleguide.create(
      brand_id: self.id,
      brand_color_1: "#007bff",
      brand_color_2: "#6c757d",
      brand_color_3: "#17a2b8",
      brand_color_4: "#28a745",
      brand_color_5: "#ffc107",
      brand_color_6: "#dc3545",
      font_primary: "Montserrat",
      font_secondary: "Open Sans",
      icon_choice: 1,
      button_choice: 1,
      form_input_choice: 1
    )
  end
```

```ruby
# model.rb

after_create_commit {EventBroadcastJob.perform_later self, Event.where(read: [false, nil], user: self.user_id).count}
```
