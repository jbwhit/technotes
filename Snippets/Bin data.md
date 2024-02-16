
```python
Nbins = 10
labels = list('abcdefghij')
pd.cut(series, Nbins) # equal width bins based on data
pd.cut(series, [23, 25, 29]) # given specified bins
pd.qcut(series, Nbins) # equal numbers per quantile bin
pd.qcut(series, Nbins, labels=labels) # label bins
```

See also: 
- [[Quantile]]
- [[Histograms]]

