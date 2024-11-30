
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

# Launch nbclassic!
uv run --with jupyter jupyter nbclassic
```


- [ ] is there a way to prune kernels so that they don't start to overflow? 
- [ ] Can I go from the pyproject.toml file to an update nbdev thing? 

```bash
#!/bin/bash

# Usage: ./setup_uv_project.sh <project_name>
PROJECT_NAME=$1

if [ -z "$PROJECT_NAME" ]; then
    echo "Please provide a project name"
    echo "Usage: ./setup_uv_project.sh <project_name>"
    exit 1
fi

# 1. Create and set up virtual environment with Python 3.12
rm -rf $PROJECT_NAME/.venv
uv venv --python 3.12 $PROJECT_NAME/.venv

# 2. Activate the virtual environment
source $PROJECT_NAME/.venv/bin/activate

# 3. Install the project in editable mode
uv pip --project $PROJECT_NAME install -e $PROJECT_NAME

# 4. Set up Jupyter kernel and start notebook
uv run ipython kernel install --user --name=$PROJECT_NAME
uv run --with jupyter jupyter nbclassic
```

```bash
chmod +x setup_uv_project.sh
./setup_uv_project.sh myproject
```

