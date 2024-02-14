

pyarrow extension backend
```python
pd.Series(x, dtype='int8[pyarrow]')
```


> [!note] 
> numpy doesn't support missing values in integers NA NAN (converts to float)

string type in pyarrow (alias for the type) `string[pyarrow]`


## Chapter 6

Get values from index

> [!note] Understand values from index
> from pg. 38
> ```python
> def get(series, idx):
>     value_idx = series['index'].index(idx)
> 	return series['data'][value_idx]
> ```


How should I declare a category type pandas pyarrow?

Matt suggests: use pandas 'category' type.


## Chapter 7




