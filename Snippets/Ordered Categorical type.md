
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

```python
months = ['Jan', 'Feb', 'Mar']
month_cat = pd.CategoricalDtype(categories=months, ordered=True)
pd.Series(months, dtype=string_pa).astype(month_cat)
```

## reorder categories

```python
(s
	.cat.add_categories(['xs', 'xl',])
	.cat.reorder_categories(['xs', 's', 'm', 'l', 'xl'],
							ordered=True)
)
```


