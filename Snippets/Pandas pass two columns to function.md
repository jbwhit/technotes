
Use lambda function to pass columns through.

```python
(
df.pipe(
	lambda df_: pd.Series(
		np.random.randint(df_.iloc[:, 0], df_.iloc[:, 1]), index=df_.index
	)
)
)
```

