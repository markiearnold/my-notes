# Git History

## Remove

### Remove large deleted file in git history, causing slow push/pull

```bash
git filter-branch --tree-filter 'rm -rf file-name.pdf' HEAD
```
