
Pandas 

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


