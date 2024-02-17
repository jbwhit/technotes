
```python
(df
	.str.extract(r'P<non_alpha>[^a-z A-Z])', expand=False)
	#or
	.str.extract(r'P<non_num>[^0-9])', expand=False) # non numeric
	.value_counts()
```

