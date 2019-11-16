# [Ransack](https://github.com/activerecord-hackery/ransack)

## Setup

Add to gemfile
```ruby 
gem 'ransack'
```

---

# Multiple models in EasyAutocomplete Search

## Step 1: Add ransack models to search
In controller define the models you would like to search.
In this case I want to search for all has_many associations to teams.

```ruby 
# teams_controller.rb
def search
  @s_collections = Collection.where(team_id: @team).ransack(name_cont: params[:q]).result(distinct: true).limit(12)
  @s_projects = Project.where(team_id: @team).ransack(name_cont: params[:q]).result(distinct: true).limit(12)
  @s_documents = Document.where(team_id: @team).ransack(name_cont: params[:q]).result(distinct: true).limit(12)
end
```

## Step 2: Force JSON for search view
```ruby
# teams_controller.rb

class TeamsController < ApplicationController
    before_action :force_json, only: [:search]
  
  private
  
    def force_json
      request.format = :json
    end
end
```

## Step 3: Install Easy AutoComplete
Install [EasyAutocomplete](http://easyautocomplete.com/) javascript and css through your asset pipeline or cdn.

## Step 4: Include Search javascript
```javascript
// app/javascripts/search.js

document.addEventListener("turbolinks:load", function() {
  var $input = $("[data-behavior='autocomplete']");
  var team_id = $("body").data("team");

  var options = {
    getValue: "name",

    url: function(phrase) {
      return "/teams/" + team_id + "/search.json?q=" + phrase;
    },

    categories: [
      {
        listLocation: "collections",
        header: "<strong>Collections</strong>",
        getValue: "name"
      },
      {
        listLocation: "projects",
        header: "<strong>Projects</strong>",
        getValue: "name"
      },
      {
        listLocation: "documents",
        header: "<strong>Documents</strong>",
        getValue: "name"
      }
    ],

    list: {
      maxNumberOfElements: 100,
      onChooseEvent: function() {
        var url = $input.getSelectedItemData().url;
        $input.val("");
        Turbolinks.visit(url);
      }
    },
    theme: "square"
  };

  $input.easyAutocomplete(options);
});
```

## Step 5: Add Search.jbuilder.js view
```javascript
// app/views/teams/search.json.jbuilder

json.collections do
  json.array!(@s_collections) do |collection|
    json.name collection.name
    json.url team_collection_path(collection.team, collection)
  end
end

json.projects do
  json.array!(@s_projects) do |project|
    json.name project.name
    json.url team_collection_project_path(project.team, project.collection, project)
  end
end

json.documents do
  json.array!(@s_documents) do |document|
    json.name document.name
    json.url project_document_path(document.project, document)
  end
end
```

## Step 6: Add to routes
```ruby
# config/routes

resources :teams do
  get :search
end
```
