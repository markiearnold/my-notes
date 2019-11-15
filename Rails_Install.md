# Install Ruby On Rails

### Installing Homebrew
Homebrew allows you to install and compile software packages easily from source.

*Open Terminal and run the following command:*
```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```


### Installing Ruby

*In Terminal run the following command:*
```
brew install rbenv ruby-build

# Add rbenv to bash so that it loads every time you open a terminal
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile
source ~/.bash_profile

# Install Ruby
rbenv install 2.5.0
rbenv global 2.5.0
ruby -v
```


### Installing Rails

*In Terminal run the following command:*
```
gem install rails -v 5.2.2
```

Rails is now installed, but in order for us to use the rails executable, we need to tell rbenv to see it:
```
rbenv rehash
```

And now we can verify Rails is installed:
```
rails -v
# Rails 5.2.2
```


### Setting Up Database
##### PostgreSQL
```
brew install postgresql
```

Once this command is finished, it gives you a couple commands to run. Follow the instructions and run them:
```
# To have launchd start postgresql at login:
brew services start postgresql
```

### Finished!
