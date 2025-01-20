
where command
```python
N = 10
topN = df.value_counts().index[:N]
df.where(df.isin(topN), "Other")
```

See also [[case_when pandas]] for `case_when` version of this. 

Plot: 

```python
top10 = df.value_counts().index[:10]
(df
	.where(df.isin(top10), 'Other')
	.value_counts()
	.plot_barh()
)
```

