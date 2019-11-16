# Routing

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
