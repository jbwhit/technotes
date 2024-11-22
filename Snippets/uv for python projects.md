
```zsh
unset GITHUB_TOKEN
gh repo create practice_2024-11-22 --private --clone


cd practice_2024-11-22
# Update uv to latest version
uv self update

# Initialize new virtual environment
uv init aucvenv
cd aucvenv

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