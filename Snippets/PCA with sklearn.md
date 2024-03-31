
```python
from sklearn.decomposition import PCA
from sklearn import set_config
set_config(transform_output='pandas')
pca = PCA()
pca.fit_transform(df)
pca.components_

# make dataframe
df = pd.DataFrame(pca.components_,
				  index=[f'pca{i}' for i in range(nums.shape[1])],
				  columns=nums.columns)

explained_ser = pd.Series(pca.explained_variance_ratio,
		 index=[f'pca{i}' for i in range(nums.shape[1])])
```

