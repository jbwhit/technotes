
Add a kernel to your conda environment (mastery in this example)

```sh
conda install -c conda-forge ipykernel
# display-name is optional
# name is used by Jupyter and will overwrite existing kernels
python -m ipykernel install --user --name=mastery --display-name "Python (more description)"
```

List kernels

```shell
jupyter kernelspec list 
```

Then simply uninstall your unwanted-kernel:

Remove kernel 

```sh
# just the kernel
jupyter kernelspec uninstall mastery

# remove env
conda env remove --name mastery
```

