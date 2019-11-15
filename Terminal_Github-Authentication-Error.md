# Terminal: Github Authentication Error

## Am I using SSH?

```bash
git remote -v 
```

* This command returns a string that starts with `https://`.  If so, view #1
* This command returns a string that starts with `git@`.  If so, view #2

1. Since we use 2-factor authentication on Github, we need to use SSH instead of HTTPS.

You can get the SSH url from the github repo:
![](https://d2y84jyh761mlc.cloudfront.net/items/3R1d3q120Y04322W0b3O/Image%202019-11-15%20at%202.55.42%20PM.png?X-CloudApp-Visitor-Id=3221729)

```bash
$ git remote remove origin 
$ git remote add origin git@github.com:user/repo.git  
```

2. I need to make sure that my SSH key is added.

```bash
$ eval "$(ssh-agent -s)"
> Example Response: Agent pid 59566
```

* If this does respond with the example response, we will use `ssh-add` below. The `-K` is to add the ssh key to keychain.

```bash
$ ssh-add -K ~/.ssh/id_rsa
```
