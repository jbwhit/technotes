
If you have a project w/ pull requests on github, 

```
git config remote.origin.fetch '+refs/pull/*:refs/remotes/origin/pull/*'
git fetch
```

You will see PR refs that you can merge (without adding their remote).