With help from: 
- https://mamba.readthedocs.io/en/latest/user_guide/mamba.html
- https://docs.conda.io/projects/conda/en/stable/commands/index.html
- https://www.imranabdullah.com/2021-08-21/Conda-and-Mamba-Commands-for-Managing-Virtual-Environments

### Installing Mamba

```bash
conda install -n base -c conda-forge mamba
```
### Adding channels

```bash
conda config --add channels fastai
conda config --add channels conda-forge
```
### Updating Mamba  [[Updating software]]

```bash
mamba update -n base mamba
```
### Creating an environment

```bash
mamba create -n ENV_NAME PACKAGE
```
### Exporting an environment

```bash
mamba env export -n ENV_NAME > ENV_NAME.yaml
conda list -e > ENV_NAME.txt
```

### Importing an environment

```bash
mamba env create --file ENV_NAME.yaml
conda create -n ENV_NAME --file ENV_NAME.txt
```

### Adding/Updating software

```bash
mamba install -n ENV_NAME PACKAGE
mamba update -n ENV_NAME --all
```

### Removing a package

```bash
mamba remove -n ENV_NAME PACKAGE
```

### Undoing changes to an environment

```bash
mamba list -n ENV_NAME --revisions
mamba install -n ENV_NAME --revision 1
```

### Show environment

```bash
conda env export --no-builds
```

### Clone an existing environment

```bash
conda create --name CLONE_ENV_NAME --clone ENV_NAME
```
### Removing an environment

```bash
mamba env remove -n ENV_NAME
conda remove --name ENV_NAME --all
```

### Deactivate the environment

```bash
mamba deactivate
```

### Viewing a list of your environments

```bash
conda info --envs
conda env list
```

### Searching for dependencies

```bash
mamba repoquery depends -a PACKAGE
```
### Finding a Package

```bash
mamba repoquery search PACKAGE
```

