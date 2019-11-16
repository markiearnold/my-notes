# Routing

## Custom methods on resource

```ruby
resources :teams do
  get :recap
  get :search
  get :settings
  resources :collections do
    get :roadmap
    resources :projects do
      get :doclist
    end
  end
end
```

## Back

```ruby
link_to 'Back', 'javascript:history.back()'
```
