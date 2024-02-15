
```python
df.clip(
		lower=df['col'].quantile(0.05),
		upper=df['col'].quantile(0.95),
)
```

