

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

Then create separate config files for work and personal:

```bash
# ~/.gitconfig-work
[user]
    name = Work Name
    email = work@example.com
    signingKey = ABCDEF1234567890

# ~/.gitconfig-personal
[user]
    name = Personal Name
    email = personal@example.com
    signingKey = 0987654321FEDCBA

```

Repositories in `~/work/` or `~/personal/` will automatically use these settings.

### Enforcing GPG-Signed Commits

Add a signing key to your Git config:

```bash
# ~/.gitconfig
[user]
    signingKey = ABCDEF1234567890
[commit]
    gpgSign = true

```


Verify commits with GPG:

1. Generate a GPG key:

```bash
gpg --full-generate-key
```
  2. Export the public key to share with teammates:
```bash
gpg --export --armor ABCDEF1234567890 > publickey.asc
```
  3. Add the key to your Git hosting service (e.g., GitHub, GitLab).
To require signed commits, add a `pre-receive` or `commit-msg` hook.

## ### **Enforcing Trust in Commit Metadata**

Use commit hooks to enforce proper user identity.

Create a `.git/hooks/commit-msg` hook:

```ash
```