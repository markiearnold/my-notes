# Terminal: Notifications

```bash
brew install terminal-notifier

# Add to ~/.bash_profile
alias notifyDone='terminal-notifier -title "Terminal" -message "Done with task!"'

# How to use in terminal
echo test ; notifyDone
```

OR without alias
```bash
echo test ; terminal-notifier -message 'finished'
```

To also say outloud 
```bash
echo test ; terminal-notifier -message 'finished' ; say finished
```

Robust solution 
```bash
To have terminal notify you when a long task is finished:

brew install terminal-notifier

# Add to ~/.bash_profile
alias notifyDone='terminal-notifier -title "Terminal" -message "Task is done!" ; say finished'

# How to use
echo testing ; notifyDone
```
