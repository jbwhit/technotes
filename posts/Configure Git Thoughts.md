
reuse recorded resolution (automatically re-fixes conflict resolution)

```
git config --global rerere.enabled true
git config --global rerere.autoUpdate true
```

stash all things with an alias

```
git config --global alias.staash 'stash --all'
```

run shell prompt from a git alias (need the leading `!`): 
gist.github.com/schacon
https://gist.github.com/schacon/e9e743dee2e92db9a464619b99e94eff
```
git config --global alias.bb !better-branch.sh
```

branches listed in columns, sorted by last touched branch

```
git config --global column.ui auto
git config --global branch.sort -committerdate
```

Always do "nice" force pushes.

```
git config --global alias.fpush push --force-with-lease
```