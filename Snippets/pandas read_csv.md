

```python
df = pd.read_csv(
	  url, 
	  dtype_backend='pyarrow', # use pyarrow types
      engine='pyarrow', # parse w/ pyarrow
     )
```


- [ ] unnamed column index=False 

recommend doing date stuff outside of read_csv. 
