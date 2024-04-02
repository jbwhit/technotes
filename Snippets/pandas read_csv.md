---
id: pandas read_csv
aliases: []
tags: []
---



```python
df = pd.read_csv(
	    url, 
	    dtype_backend='pyarrow', # use pyarrow types
      engine='pyarrow', # parse w/ pyarrow
    )
```


- [ ] unnamed column index=False; also `index_col=0` to recover from error.

recommend doing date stuff outside of read_csv. 
