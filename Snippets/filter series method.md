
filters on the index
```python
series.filter(items=['First', 'Second'],# exact
			  like='st', # partial string matching "past" would match
			  regex='^Aw', 
			 )
```

