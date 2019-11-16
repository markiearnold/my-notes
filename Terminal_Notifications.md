# Terminal: Notifications

```
brew install terminal-notifier

# Add to ~/.bash_profile
alias notifyDone='terminal-notifier -title "Terminal" -message "Done with task!"'

# How to use in terminal
echo test ; notifyDone
```

OR without alias
```
echo test ; terminal-notifier -message 'finished'
```

To also say outloud 
```
echo test ; terminal-notifier -message 'finished' ; say finished
```

Robust solution 
```
To have terminal notify you when a long task is finished:

brew install terminal-notifier

# Add to ~/.bash_profile
alias notifyDone='terminal-notifier -title "Terminal" -message "Task is done!" ; say finished'

# How to use
echo testing ; notifyDone
```
