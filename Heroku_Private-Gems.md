# Installing a gem from a private GitHub repo (Heroku)
This is a little guide on how to install private gems hosted in GitHub on the Heroku platform.

0. Getting started
To follow this guide, you need Bundler +1.11.

```
$ bundle --version Bundler version 1.11.2
```

1. Get your OAuth Token from GitHub
To authenticate Bundler to GitHub, you will need an OAuth token. You can follow this guide to create a new one.

2. Setting up your credentials
To set up your credentials, use bundle-config:

```
$ bundle config GITHUB__COM myoauthtoken:x-oauth-basic
```

If you want to apply this configuration only to your current project, do this instead:

```
$ bundle config --local GITHUB__COM myoauthtoken:x-oauth-basic
```

3. Install your dependencies
Add your private gem to the Gemfile:

```
gem "mygem", git: "https://github.com/user/mygem.git"
```

Install the gem dependencies using bundle install:

```
$ bundle install
Fetching https://github.com/user/mygem.git
Fetching gem metadata from https://rubygems.org/......... 
Fetching version metadata from https://rubygems.org/.. 
Using mygem 1.0.0 from https://github.com/user/mygem.git (at master@bc4adfb)
Using bundler 1.11.2
Bundle complete! 1 Gemfile dependency, 2 gems now installed.
```

Notice that your credentials aren’t stored in the Gemfile or the generated Gemfile.lock.
