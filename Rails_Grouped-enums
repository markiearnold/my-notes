# Rails: Grouped Enums
To prevent created robust schema for items that do not need to be managed in the UI, you can use enums.  One need I wanted, was to group enum values by a type.

For example:
* Roadmap Types: UX, PM, OKR, NONE
* Phases: Should be related to each type.  ux_phase1, ux_phase2, pm_phase1, okr_phase1, etc

## Add a concern
For enums to be used across models, use them in a concern
```ruby
# app/models/concerns/phaseable.rb
module Phaseable
  extend ActiveSupport::Concern
  included do
    enum phase: {
      ux_research: 'ux_research',
      ux_design: 'ux_design',
      ux_prototype: 'ux_prototype',
      ux_handoff: 'ux_handoff',
      ux_closed: 'ux_closed',
      pm_new: 'pm_new',
      pm_planning: 'pm_planning',
      pm_execution: 'pm_execution',
      pm_closure: 'pm_closure',
      pm_monitoring: 'pm_monitoring',
      pm_closed: 'pm_closed',
      okr_draft: 'okr_draft',
      okr_score: 'okr_score',
      okr_planning: 'okr_planning',
      okr_execution: 'okr_execution',
      okr_closed: 'okr_closed',
    }, _suffix: true
  end
end
```

## Add enums to model
```ruby
class Project < ApplicationRecord
  include Phaseable
end
```

## Add column to database for Model
We will be adding the enum as "string"
This is because how we have it structured above. If only saved as integer, the order and names of the enums can become more fragile overtime and cannot be changed.

```ruby
class AddPhaseToProjects < ActiveRecord::Migration[5.2]
  def change
    add_column :hud_projects, :phase, :string, default: 'none'
  end
end
```

## Retrieve subset of enums by type
In order to fill a form select with only options related to a certain type (ux, okr, pm, etc), we create this method in the model
```ruby 
# app/models/project.rb
def self.phase_options(roadmap)
  filtered_phases = self.phases.select { |element| element.include?("#{roadmap}_") }
  filtered_phases.map { |k,v| [k, v] }
end
```

## Example Form Select
```erb
<div class="form-group label-inside">
  <%= form.label :phase %>
  <% phase_option_choices = Project.phase_options(@project.roadmap) %>
  <%= form.select :phase, options_for_select(phase_option_choices, @project.phase), 
      {include_blank: 'Select Phase'}, class: 'form-control' %>
</div>
```
