# Rails: Custom table names 

## Define table name in model
```ruby 
class Team < ApplicationRecord
  self.table_name = "hud_teams"
end
```

## Update associations
For belongs_to and has_many associations, define `foreign_key`.

In this example, both team and projects have custom table names as well (hud_teams, hud_projects)
```ruby
class Collection < ApplicationRecord
  self.table_name = "hud_collections"
  belongs_to :team, foreign_key: :team_id
  has_many :projects, foreign_key: :collection_id
end
```

## Association migrations
Foreign Key should be added by `to_table` options. See below.
```ruby 
class AddTeamRefToCollections < ActiveRecord::Migration[5.2]
  def change
    add_reference :hud_collections, :team, foreign_key: { to_table: :hud_teams }
  end
end
```
