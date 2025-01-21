# Single Variable
## Categorical

```python
def categorical_counts(df, column):
    # Plot
    sns.countplot(data=df, x=column)
```

```python
def generalize_topn(ser, n=5, other='Other'):
	topn = ser.value_counts().index[:n]
	if isinstance(ser.dtype, pd.CategoricalDtype):
		ser = ser.cat.set_categories(
			topn.set_categories(list(topn) + [other]))
	return ser.where(ser.isin(topn), other)

df.pipe(generalize_topn, n=20, other='NA')
```
## Numerical 

```python
def numerical_summary(df, column):
    # Plot
    sns.histplot(data=df, x=column, kde=True)


	# Plot
	diamonds = sns.load_dataset("diamonds")
	clarity_ranking = ["I1", "SI2", "SI1", "VS2", "VS1", "VVS2", "VVS1", "IF"]
	# Plot
	sns.boxenplot(
		diamonds, x="clarity", y="carat",
		color="b", order=clarity_ranking, width_method="linear",
	)
	# Plot ecdf
	sns.displot(
	    mpg,
	    x="displacement", col="origin", hue="model_year",
	    kind="ecdf", aspect=.75, linewidth=2, palette=cmap,
	)
```

```python
def numerical_summary(df, column, group_by=None):
    # ECDF
    if group_by is None:
        # Single ECDF
        data = np.sort(df[column].dropna())
        n = len(data)
        cumulative_prob = np.arange(1, n + 1) / n
        ax2.plot(data, cumulative_prob, linewidth=2)
    else:
        # Grouped ECDF
        colors = sns.color_palette()[:df[group_by].nunique()]
        for i, (name, group) in enumerate(df.groupby(group_by)):
            data = np.sort(group[column].dropna())
            n = len(data)
            cumulative_prob = np.arange(1, n + 1) / n
            ax2.plot(data, cumulative_prob, 
                    label=f'{group_by}={name}',
                    color=colors[i],
                    linewidth=2)
        ax2.legend()
```
## 2 Categorical

```python
def categorical_cross_tab(df, col1, col2):
    """Create cross-tabulation and stacked bar plot for two categorical variables"""
    # Create cross-tabulation
    ctab = pd.crosstab(df[col1], df[col2], normalize='index')
    # Plot
	ctab.plot(kind='bar', stacked=True)
```

## 2 Numerical

```python
def numerical_correlation(df, col1, col2):
    # Calculate correlation
    corr = df[col1].corr(df[col2])
    # Plot
    sns.scatterplot(data=df, x=col1, y=col2)
    # Plot hexbin with marginals
	x = rs.gamma(2, size=1000)
	y = -.5 * x + rs.normal(size=1000)
	sns.jointplot(x=x, y=y, kind="hex", color="#4CB391")
	# Plot correlation
	d = pd.DataFrame(data=rs.normal(size=(100, 26)),
	                 columns=list(ascii_letters[26:]))
	# Compute the correlation matrix
	corr = d.corr()
	# Generate a mask for the upper triangle
	mask = np.triu(np.ones_like(corr, dtype=bool))
	cmap = sns.diverging_palette(230, 20, as_cmap=True)
	sns.heatmap(corr, mask=mask, cmap=cmap, vmax=.3, center=0,
	            square=True, linewidths=.5, cbar_kws={"shrink": .5})
```

## Categorical + Numerical

```python
def pivot_analysis(df, cat_col, num_col):
    # Create pivot table
    pivot = df.pivot_table(
        values=num_col,
        index=cat_col,
        aggfunc=['mean', 'count', 'std']
    )
    sns.boxenplot(data=df, x=cat_col, y=num_col)
```

```python
def faceted_analysis(df, cat_col, num_col):
	# Plot
    g = sns.FacetGrid(df, col=cat_col, col_wrap=3)
    g.map(sns.histplot, num_col)

	# Grouped violinplots with split violins
	# Draw a nested violinplot and split the violins for easier comparison
	sns.violinplot(data=tips, x="day", y="total_bill", hue="smoker",
	               split=True, inner="quart", fill=False,
	               palette={"Yes": "g", "No": ".35"})
```