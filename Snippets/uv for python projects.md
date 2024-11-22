
```zsh
#!/usr/bin/env zsh

# Generate repository name with current date
REPO_NAME="practice_$(date '+%Y-%m-%d')"

# Ensure GitHub token is not active for repo creation
unset GITHUB_TOKEN

# Create and clone private GitHub repository
echo "Creating repository: $REPO_NAME"
gh repo create "$REPO_NAME" --private --clone

# Navigate to repository directory
cd "$REPO_NAME" || exit 1

# Update uv to latest version
uv self update

# Initialize new virtual environment
uv init --python 3.12 aucvenv
cd aucvenv || exit 1

# Install Jupyter-related packages
uv add jupyter jupyterlab notebook nbclassic

# Install data science and visualization packages
uv add matplotlib pandas seaborn pillow scikit-learn
uv add torch torchvision

# Install development and code quality tools
uv add black ruff
uv add --dev ipykernel
uv add tqdm pyparsing nbdev

# Install dependencies from requirements file (if needed)
uv add -r ../requirements.txt

# Set up IPython kernel for Jupyter
uv run ipython kernel install --user --name=aucenv

# Launch Jupyter Lab
uv run --with jupyter jupyter lab
```


- [ ] is there a way to prune kernels so that they don't 