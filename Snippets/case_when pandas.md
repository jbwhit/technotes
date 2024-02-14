
```python
# example from Effective Pandas 2
(make
	  .case_when(caselist=[
		 (make.isin(top5), make),
		 (make.isint(top10), 'Top10'),
		 (pd.Series(True, index=make.index), 'Other')])
)
```

