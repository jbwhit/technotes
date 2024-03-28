---
id: case_when pandas
aliases:
  - example from Effective Pandas 2
tags: []
---


```python
# example from Effective Pandas 2
(make
	  .case_when(caselist=[
		 (make.isin(top5), make),
		 (make.isin(top10), 'Top10'),
		 (pd.Series(True, index=make.index), 'Other')])
)
```

See also [[Top N with remaining changed to "other"]] using `where` instead of `case_when`. 