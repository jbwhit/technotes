
where command
```python
N = 10
topN = df.value_counts().index[:N]
df.where(df.isin(topN), "Other")
```

