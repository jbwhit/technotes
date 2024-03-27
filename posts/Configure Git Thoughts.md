
Setup `gh` -- https://cli.github.com/ 

```sh
❯ gh auth login
? What account do you want to log into? GitHub.com
? What is your preferred protocol for Git operations on this host? SSH
? Upload your SSH public key to your GitHub account? 
? Title for your SSH key: GitHub CLI
? How would you like to authenticate GitHub CLI? Login with a web browser
! First copy your one-time code: XXXX-XXXX
Press Enter to open github.com in your browser...
✓ Authentication complete.
- gh config set -h github.com git_protocol ssh
✓ Configured git protocol
✓ SSH key already existed on your GitHub account: 
✓ Logged in as username
```

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