
```bash
mamba install -c conda-forge ydata-profiling
```

```python
from ydata_profiling import ProfileReport

profile = ProfileReport(df, title="Pandas Profiling Report")

# files
profile.to_file("your_report.html")

# interactive
profile.to_widgets()

# iframe
profile.to_notebook_iframe()

```



[[missingno]] -- missing number visualizations

