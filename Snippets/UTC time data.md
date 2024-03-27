convert to a time zone.
```python
col = pd.Series(
    [
        "2015-03-08 08:00:00+00:00",
    ]
)
utc_s = pd.to_datetime(col, utc=True)

utc_s.dt.tz_convert('America/Denver')
local.dt.tz_convert('UTC')
```