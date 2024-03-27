The `.transform` allows the aggregate to land on the original index
gives the percentage of quarterly snow that fell each day

```python
(snow
.div(snow
	.resample('QE')
	.transform('sum'))
.mul(100)
.fillna(0)
)
```