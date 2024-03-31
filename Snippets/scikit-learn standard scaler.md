
```python
from sklearn.preprocessing import StandardScaler

ss = StandardScalar()
# to return dataframe but really import better
ss.set_output(transform='pandas')
res = (ss.fit_transform(nums))
```