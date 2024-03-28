
#pandas 

```python
make_type = pd.CategoricalDtype(
	categories=sorted(make.unique()), ordered=True)
ordered_make = make.astype(make_type)								
```

if you want as ordered in the original series: 

```python
(make.astype('category').cat.as_ordered())
```

