using parameter expansion can do a pattern removal

```bash
for notebook in *.ipynb; do
  cp "$notebook" "${notebook%.ipynb}-after.ipynb"
done
```

The `%` removes the .ipynb from the end, and simply replaces it.


```bash
${variable/pattern/replacement} # replaces the first occurrence.
${variable//pattern/replacement} # replaces all occurrences.
```

