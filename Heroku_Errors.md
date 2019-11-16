# Heroku: Errors

## Issues
```bash
remote:  !     Could not detect rake tasks
remote:  !     ensure you can run `$ bundle exec rake -P` against your app
remote:  !     and using the production group of your Gemfile.
remote:  !     Activating bundler (2.0.1) failed:
remote:  !     Could not find 'bundler' (2.0.1) required by your /tmp/build_94d6a4f5d4fbb862672998d5d06d2506/Gemfile.lock.
remote:  !     To update to the latest version installed on your system, run `bundle update --bundler`.
remote:  !     To install the missing version, run `gem install bundler:2.0.1`
remote:  !     Checked in 'GEM_PATH=/tmp/build_94d6a4f5d4fbb862672998d5d06d2506/vendor/bundle/ruby/2.7.0', execute `gem env` for more information
remote:  !     
```

## Fix
```bash
gem install bundler -v 2.0.2
bundle update --bundler
# commit changes & redeploy
```

## In order for your Webpacker app to run on Heroku, you’ll need to do a bit of configuration before hand.

```bash
heroku create my-webpacker-heroku-app
heroku addons:create heroku-postgresql:hobby-dev
heroku buildpacks:add heroku/nodejs
heroku buildpacks:add heroku/ruby
git push heroku master
```


[ruby on rails 5 - Heroku installs Bundler then throws error Bundler 2.0.1 - Stack Overflow](https://stackoverflow.com/questions/56680065/heroku-installs-bundler-then-throws-error-bundler-2-0-1)
