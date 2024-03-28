#pandas 

```python
def generalize_topn(ser, n=5, other='Other'):
	topn = ser.value_counts().index[:n]
	if isinstance(ser.dtype, pd.CategoricalDtype):
		ser = ser.cat.set_categories(
			topn.set_categories(list(topn) + [other]))
	return ser.where(ser.isin(topn), other)

df.pipe(generalize_topn, n=20, other='NA')
```

