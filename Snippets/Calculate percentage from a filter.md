
```python
(df
  .gt(20) # greater than 
  .mul(100) # make percentage
  .mean() # 0 / 1 from the `gt` means this is percentage
)
```

