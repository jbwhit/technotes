
```python
mask = series1 > 20
series1.iloc[mask.to_numpy()] # need to convert list or an array
series1.iloc[list(mask)] # need to convert list or an array
```

