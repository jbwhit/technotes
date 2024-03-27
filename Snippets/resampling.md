If you have a series with dates in the index, you can use `.resample`.

```python
(snow
 .resample('ME')
 .max()
)
```

ME is month end