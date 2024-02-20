
```
git clone --bare git@repo 
```

then, in the bare repo:

```
git worktree add <branch name>
git worktree add <branch name 2>

git worktree remove <branch name>
```

and they will appear in sub-folders.

