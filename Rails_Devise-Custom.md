# [Devise](https://github.com/plataformatec/devise) Custom Service Login

## Add fields to database
```ruby
class AddCustomFieldsToUser < ActiveRecord::Migration[5.2]
  def change
    add_column :users, :custom_id, :integer
    add_column :users, :avatar_url, :string
    add_column :users, :avatar_thumb_url, :string
    add_column :users, :first_name, :string
    add_column :users, :middle_name, :string
    add_column :users, :last_name, :string
    add_column :users, :nick_name, :string
    add_column :users, :preferred_name, :string
    add_column :users, :goes_by, :string
    add_column :users, :title, :string
  end
end
```

## Update User model
Please note, below we are also adding the options `user.name` and `user.full_name`
```ruby 
class User < ApplicationRecord
  devise :database_authenticatable, :rememberable, :trackable

  def name
    return self.goes_by
  end

  def full_name
    return "#{self.goes_by} #{self.last_name}"
  end

  def self.sign_in_or_create_user(sign_in_params)
     require 'net/http'
     uri = URI.parse("https://custom.website.com/api/v1/users/login")
     request = Net::HTTP::Get.new(uri)
     request.basic_auth(sign_in_params[:email], sign_in_params[:password])
     req_options = {
       use_ssl: uri.scheme == "https",
     }

     response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
       http.request(request)
     end

     if response.code == "200"
       user = self.find_or_create_user(response.body)
       return true, user
     else
       return false, JSON.parse(response.body)
     end
   end

   def self.find_or_create_user(user_info)
     user_info = JSON.parse(user_info)
     user = find_or_initialize_by(custom_id: user_info['id'].to_i)
     user.first_name = user_info['first_name']
     user.middle_name = user_info['middle_name']
     user.last_name = user_info['last_name']
     user.nick_name = user_info['nick_name']
     user.preferred_name = user_info['preferred_name']
     user.goes_by = user_info['goes_by']
     user.email = user_info['email']
     user.avatar_url = user_info['avatar_url']
     user.avatar_thumb_url = user_info['avatar_thumb_url']
     user.title = user_info['title']
     user.save
     return user
   end
end
```

### Override sessions controller
```ruby
# app/controllers/users/sessions_controller.rb
class Users::SessionsController < Devise::SessionsController
  def create
    success, user = User.sign_in_or_create_user(sign_in_params)
    if success
      sign_in(:user, user)
      redirect_to :root, flash: { success: "Welcome #{user.goes_by}" }
    else
      redirect_back fallback_location: root_path, flash: { error: user["error"] }
    end
  end

  def configure_sign_in_params
    devise_parameter_sanitizer.permit(:sign_in, keys: [:attribute])
  end
end
```

### Add to routes
```ruby 
Rails.application.routes.draw do
  devise_for :users, controllers: {
    sessions: 'users/sessions'
  }
end
```


## Options
| Option        | Description           |
| ------------- |:-------------:|
| name      | Shorthand for goes_by |
| full_name      | Shorthand for goes_by last_name      |
| &nbsp; | &nbsp; |
| first_name | User's first name in Custom |
| middle_name | User's middle name in Custom |
| last_name | User's last name in Custom |
| nick_name | User's nickname in Custom |
| preferred_name | Name preferred in Custom |
| goes_by | User's name they go by in Custom |
| email | User's Custom email address |
| title | User's title in Custom |
| avatar_url | User's Custom avatar url |
| avatar_thumb_url | User's Custom avatar thumb url |
