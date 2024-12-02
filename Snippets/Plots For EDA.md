

# Single Variable
## Categorical

```python
def categorical_counts(df, column):
    """Create value counts and plot for categorical variable"""
    plt.figure(figsize=(10, 5))
    sns.countplot(data=df, x=column)
    plt.xticks(rotation=45)
    plt.title(f'Distribution of {column}')
    plt.tight_layout()
    
    # Print counts
    print(f"\nValue counts for {column}:")
    print(df[column].value_counts())
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
    """Create summary statistics and distribution plot for numerical variable"""
    # Summary statistics
    stats = df[column].describe()
    print(f"\nSummary statistics for {column}:")
    print(stats)
    
    # Create distribution plot
    plt.figure(figsize=(10, 5))
    sns.histplot(data=df, x=column, kde=True)
    plt.title(f'Distribution of {column}')
    plt.tight_layout()
```

A bit more

```python
def numerical_summary(df, column, group_by=None):
    """
    Create summary statistics and distribution plots for numerical variable,
    optionally grouped by a categorical variable.
    """
    # Summary statistics
    stats = df[column].describe()
    print(f"\nSummary statistics for {column}:")
    print(stats)
    
    # Create figure with subplots for histogram and ECDF
    fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(15, 5))
    
    # Histogram with KDE
    sns.histplot(data=df, x=column, kde=True, ax=ax1)
    ax1.set_title(f'Distribution of {column}')
    
    # ECDF
    if group_by is None:
        # Single ECDF
        data = np.sort(df[column].dropna())
        n = len(data)
        cumulative_prob = np.arange(1, n + 1) / n
        ax2.plot(data, cumulative_prob, linewidth=2)
    else:
        # Grouped ECDF
        colors = sns.color_palette()[:len(df[group_by].unique())]
        for i, (name, group) in enumerate(df.groupby(group_by)):
            data = np.sort(group[column].dropna())
            n = len(data)
            cumulative_prob = np.arange(1, n + 1) / n
            ax2.plot(data, cumulative_prob, 
                    label=f'{group_by}={name}',
                    color=colors[i],
                    linewidth=2)
        ax2.legend()
    
    ax2.set_title(f'ECDF of {column}')
    ax2.set_xlabel(column)
    ax2.set_ylabel('Cumulative Probability')
    ax2.grid(True, alpha=0.3)
    
    plt.tight_layout()

```
# Double variable
## 2 Categorical

```python
def categorical_cross_tab(df, col1, col2):
    """Create cross-tabulation and stacked bar plot for two categorical variables"""
    # Create cross-tabulation
    ctab = pd.crosstab(df[col1], df[col2], normalize='index')
    print("\nCross-tabulation:")
    print(ctab)
    
    # Create stacked bar plot
    plt.figure(figsize=(10, 6))
    ctab.plot(kind='bar', stacked=True)
    plt.title(f'{col1} vs {col2}')
    plt.xticks(rotation=45)
    plt.tight_layout()

```

## 2 Numerical

```python
def numerical_correlation(df, col1, col2):
    """Create correlation analysis and scatter plot for two numerical variables"""
    # Calculate correlation
    corr = df[col1].corr(df[col2])
    print(f"\nCorrelation between {col1} and {col2}: {corr:.3f}")
    
    # Create scatter plot
    plt.figure(figsize=(10, 6))
    sns.scatterplot(data=df, x=col1, y=col2)
    plt.title(f'{col1} vs {col2} (correlation: {corr:.3f})')
    plt.tight_layout()
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