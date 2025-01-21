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
# Double variable
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
    # hexbin with marginals
    import numpy as np
	import seaborn as sns
	sns.set_theme(style="ticks")
	
	rs = np.random.RandomState(11)
	x = rs.gamma(2, size=1000)
	y = -.5 * x + rs.normal(size=1000)
	
	sns.jointplot(x=x, y=y, kind="hex", color="#4CB391")
```

## Categorical + Numerical

```python
def pivot_analysis(df, cat_col, num_col):
    """Create pivot table analysis for numerical and categorical variables"""
    # Create pivot table
    pivot = df.pivot_table(
        values=num_col,
        index=cat_col,
        aggfunc=['mean', 'count', 'std']
    )
    print(f"\nPivot table analysis of {num_col} by {cat_col}:")
    print(pivot)
    
    # Create box plot
    plt.figure(figsize=(10, 6))
    sns.boxplot(data=df, x=cat_col, y=num_col)
    plt.xticks(rotation=45)
    plt.title(f'Distribution of {num_col} by {cat_col}')
    plt.tight_layout()
```

```python
def faceted_analysis(df, cat_col, num_col):
    """Create faceted histogram for numerical variable by categorical variable"""
    plt.figure(figsize=(12, 6))
    g = sns.FacetGrid(df, col=cat_col, col_wrap=3)
    g.map(sns.histplot, num_col)
    plt.suptitle(f'Distribution of {num_col} by {cat_col}', y=1.02)
    plt.tight_layout()
```