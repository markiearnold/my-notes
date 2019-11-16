# Terminal: Yarn

## Yarn won't update

```bash
brew upgrade yarn
brew link --overwrite yarn
```

Then try `yarn -v`


## Install Yarn 1.13.0

```bash
brew unlink yarn || true
brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/4cb921e813c02a2a294d5da767c0a24b05de7b1e/Formula/yarn.rb
brew switch yarn 1.13.0
```
