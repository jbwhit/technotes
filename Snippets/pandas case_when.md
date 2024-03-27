
Use boolean masks to add cases when to apply different results

```python
winter = (snow.index.quarter == 1) | (snow.index.quarter == 4)
(snow
  .case_when([(winter & snow.isna(), snow.interpolate()),
			  (~winter & snow.isna(), 0)
  ])
)
```

