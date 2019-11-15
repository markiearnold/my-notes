# Create Schema

## Create Models
Exclude columns that would be Foriegn Keys

```bash
# Example: Table Page with column "title"
rails g model Page title:string
rails g model Category name:string
```

## Generate Associations
Example: *Pages* can belong to a *category*.

*Page association*
In your `models/page.rb` file, add association

```bash
class Page < ApplicationRecord
  belongs_to :category
end
```

*Category association*
In your `models/category.rb` file, add association

```bash
class Category < ApplicationRecord
  has_many :pages
end
```

*Create migrations with associations*

```bash
rails g migration AddCategoryRefToPages category:references
```


## Scaffold for Models
Scaffold controller and views for models

```bash
rails g scaffold_controller Page title category_id
rails g scaffold_controller Category name
```

## Migrate Database to implement changes

```bash
rails db:migrate
```
