Env

```bash
# First, make sure you’re in the root of the nbdev repo
cd ~/projects/githubcontributions/nbdev

# Set up a virtual environment
python3 -m venv .venv
source .venv/bin/activate

# Upgrade pip (optional but recommended)
pip install --upgrade pip

# Install nbdev locally
pip install -e ".[dev]"

nbdev_install_hooks


```

Development

```
concurrent.futures.process.BrokenProcessPool: A process in the process pool was terminated abruptly while the future was running or pending.
```

```bash
OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES nbdev_prepare
```

