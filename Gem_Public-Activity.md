# [Public Activity](https://github.com/chaps-io/public_activity)

## Setup

Add to Gemfile
```ruby
gem 'public_activity'
```

## Models

Add to Model
```ruby 
class Article < ActiveRecord::Base
  include PublicActivity::Model
  tracked
end
```

To have `owner` always default to devise's current_user
```ruby 
class Article < ActiveRecord::Base
  include PublicActivity::Model
  tracked owner: Proc.new{ |controller, model| controller.current_user }
end
```

## Displaying Activity

```ruby
# Controller
def index
  @activities = PublicActivity::Activity.all
end
```

and in your views:
```erb
<%= render_activities(@activities) %>
```

## Work with [acts_as_paranoid](https://github.com/ActsAsParanoid/acts_as_paranoid) gem

Add to config/initializers
```ruby
# config/initializers/public_activity.rb

module PublicActivity
  module ORM
    module ActiveRecord
      class Activity < ::ActiveRecord::Base
        include Renderable
        self.table_name = PublicActivity.config.table_name

        # Define polymorphic association to the parent
        belongs_to :trackable, :polymorphic => true, :with_deleted => true
        # Define ownership to a resource responsible for this activity
        belongs_to :owner, :polymorphic => true, :with_deleted => true
        # Define ownership to a resource targeted by this activity
        belongs_to :recipient, :polymorphic => true, :with_deleted => true
        # Serialize parameters Hash
        serialize :parameters, Hash

        if ::ActiveRecord::VERSION::MAJOR < 4 || defined?(ProtectedAttributes)
          attr_accessible :key, :owner, :parameters, :recipient, :trackable
        end
      end
    end
  end
end
```

## Custom Activities

### Has many associations to tracked Modal
If the action is taken on a has_many relationship, you can set the recipient to the assocation, and use params to set the specific url to the associated record (nested routing).

##### Example: 
`trackable`: Project
`recipient` : Document
`owner` : current_user

```ruby
@project.create_activity action: 'document_create', 
    params: {url: project_document_path(@document.project, @document)}, recipient: @document
```

---

### Showing "what changed" on an activity update

On the controller update method, you can add the param `changes: @document.previous_changes`. View Rails [dirty methods](https://apidock.com/rails/ActiveModel/Dirty/previous_changes) for more details.

```ruby
# document_controller.rb update method
@project.create_activity action: 'document_update', 
    params: {changes: @document.previous_changes, url: project_document_path(@document.project, @document)}, 
    recipient: @document
```

And using a helper to help format those changes for the feed.
```ruby
def activity_changes(params)
  all_changes = []
  apply_fields = %w(name content)
  if !params[:changes].nil?
    params[:changes].each do |field_change|
      if apply_fields.include? field_change[0]
        old_full_value = field_change[1][0]
        new_full_value = field_change[1][1]
        changes_details = {
          "field" => field_change[0],
          "old_value" => strip_tags(old_full_value),
          "new_value" => strip_tags(new_full_value)
        }
        all_changes.push changes_details
      end
    end
  end
  all_changes
end
```

## Group Activity by Trackable model
In this case, I am tracking projects. I want to get activity for all projects that belongs_to a single team.
```ruby
# Retrieve an array of project ids for all projects that belongs to team
@project_array = Project.where(team: @team).where(:created_at => @start_date..@end_date).pluck(:id).uniq
@activities = PublicActivity::Activity.where(trackable_id: @project_array).group_by{|model| [model.trackable] }.uniq
```
