

## Use SSH Configurations

Set up distinct SSH identities in your `~/.ssh/config`:

```bash
# ~/.ssh/config
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_work

Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_personal

```

When cloning: 

```bash
git clone git@github-work:your-work-repo.git
git clone git@github-personal:your-personal-repo.git
```

## Use `includeIf` in Git Config

Use `includeIf` to apply configurations based on directory:

```bash
# ~/.gitconfig
[user]
    name = Default Name
    email = default@example.com

[includeIf "gitdir:~/work/"]
    path = ~/.gitconfig-work

[includeIf "gitdir:~/personal/"]
    path = ~/.gitconfig-personal

```