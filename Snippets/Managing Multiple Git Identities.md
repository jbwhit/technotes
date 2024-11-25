## SSH Configuration Setup

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

Clone repositories using configured hosts:
```bash
git clone git@github-work:your-work-repo.git
git clone git@github-personal:your-personal-repo.git
```

## Directory-Based Git Configuration

Use `includeIf` to automatically switch identities based on project directories:

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

Create separate config files:

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

## Advanced SSH Integration

For more granular control, use Git URL rewriting:

```bash
# ~/.gitconfig
[url "git@work-github:"]
    insteadOf = work-github:
[url "git@personal-github:"]
    insteadOf = personal-github:
```

## Environment Variables for Temporary Overrides

Useful for temporary session changes:

```bash
# Set temporary identity
export GIT_AUTHOR_NAME="Temporary User"
export GIT_AUTHOR_EMAIL="temp@example.com"
export GIT_COMMITTER_NAME="Temporary User"
export GIT_COMMITTER_EMAIL="temp@example.com"

# Reset to defaults
unset GIT_AUTHOR_NAME
unset GIT_AUTHOR_EMAIL
unset GIT_COMMITTER_NAME
unset GIT_COMMITTER_EMAIL
```

## Repository-Specific SSH Command

Configure SSH identity for a single repository:

```bash
cd ~/work-projects/repo
git config core.sshCommand "ssh -i ~/.ssh/id_rsa_work"
```

## Security Enforcement

### GPG Signing Setup

```bash
# Generate GPG key
gpg --full-generate-key

# Export public key
gpg --export --armor ABCDEF1234567890 > publickey.asc

# Configure Git to sign commits
[commit]
    gpgSign = true
```

### Identity Verification Hook

```bash
#!/bin/bash
# .git/hooks/pre-commit
expected_email="work.email@company.com"
actual_email=$(git config user.email)

if [ "$actual_email" != "$expected_email" ]; then
    echo "Error: User email is not set to $expected_email"
    exit 1
fi

# Make executable
chmod +x .git/hooks/pre-commit
```

Alternative commit-msg hook for company email enforcement:

```bash
#!/bin/bash
# .git/hooks/commit-msg
commit_email=$(git config user.email)

if [[ "$commit_email" != *"@company.com" ]]; then
    echo "Error: Commits must use a company email."
    exit 1
fi

chmod +x .git/hooks/commit-msg
```

