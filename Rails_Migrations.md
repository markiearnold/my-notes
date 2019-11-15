# Rails: Migrations

## Add

#### Add Column to existing model

```ruby
rails g migration AddAddressToUser address:string
rake db:migrate
```

## Delete

#### Force Delete and Children

```ruby
drop_table :accounts, force: :cascade
```

#### Remove Column from existing model

```ruby
rails g migration RemoveCountryFromSampleApps country:string
rails db:migrate
```

## Associations

#### Remove Association in Database

```ruby
def self.up
  remove_foreign_key :guideline_types, :guideline_groups
end

def self.down
  add_foreign_key :guideline_types, :guideline_groups
end
```
