## **Matrices**

```python
import numpy as np

# Create matrices
A = np.array([[1, 2], [3, 4]])    # 2x2 matrix
B = np.ones((2, 2))               # Matrix of ones
C = np.zeros((3, 3))              # Matrix of zeros
D = np.eye(3)                     # Identity matrix
E = np.random.rand(2, 2)          # Random matrix

# Matrix shape and size
shape = A.shape                   # (rows, columns)
size = A.size                     # Total number of elements

# Matrix transpose
A_T = A.T                         # Transpose of A

# Determinant
det = np.linalg.det(A)

# Rank
rank = np.linalg.matrix_rank(A)

# Trace
trace = np.trace(A)               # Sum of diagonal elements

# Inverse
A_inv = np.linalg.inv(A)          # Only if A is square and invertible

# Element-wise operations
C = A + B                         # Addition
D = A - B                         # Subtraction
E = A * B                         # Element-wise multiplication
F = A / B                         # Element-wise division

# Matrix multiplication
G = np.dot(A, B)                  # Dot product
H = A @ B                         # Preferred syntax for matrix multiplication

# Matrix power
P = np.linalg.matrix_power(A, 3)  # A^3

# Broadcasting
scaled = 2 * A                    # Scalar multiplication

# Solve Ax = b
x = np.linalg.solve(A, np.array([1, 2]))  # A must be square and invertible

# Eigenvalues and eigenvectors
eigenvalues, eigenvectors = np.linalg.eig(A)

# Singular Value Decomposition (SVD)
U, S, V = np.linalg.svd(A)

# QR decomposition
Q, R = np.linalg.qr(A)

# Cholesky decomposition
L = np.linalg.cholesky(A)          # A must be symmetric and positive definite

# Reshape matrix
A_reshaped = A.reshape((4, 1))

# Concatenate matrices
horizontal_stack = np.hstack([A, B])
vertical_stack = np.vstack([A, B])

# Sum over rows/columns
row_sum = A.sum(axis=1)            # Sum of each row
col_sum = A.sum(axis=0)            # Sum of each column

# Maximum/Minimum
row_max = A.max(axis=1)
col_min = A.min(axis=0)
```

## Pandas

```python
# From dictionary
data = {'Name': ['Alice', 'Bob'], 'Age': [25, 30]}
df = pd.DataFrame(data)

# From CSV
df = pd.read_csv('file.csv')

# From NumPy array
arr = np.array([[1, 2], [3, 4]])
df = pd.DataFrame(arr, columns=['A', 'B'])

df.head(n=5)                # First n rows
df.tail(n=5)                # Last n rows
df.info()                   # Summary of DataFrame
df.describe()               # Statistical summary
df.shape                    # Dimensions of DataFrame (rows, columns)
df.columns                  # Column names
df.dtypes                   # Data types of columns
df.isnull().sum()           # Count missing values per column

# Select columns
df['column_name']           # Single column as Series
df[['col1', 'col2']]        # Multiple columns as DataFrame

# Select rows
df.loc[row_index]           # Select row by label
df.iloc[row_index]          # Select row by position

# Filter rows
df[df['Age'] > 25]          # Rows where Age > 25
df[(df['Age'] > 25) & (df['Name'] == 'Alice')]  # Complex condition

# Query method
df.query('Age > 25 & Name == "Alice"') 

# Add new column
df['New_Col'] = df['Age'] * 2

# Modify existing column
df['Age'] = df['Age'] + 1

# Apply custom function
df['Age_Squared'] = df['Age'].apply(lambda x: x**2)

# Rename columns
df.rename(columns={'Old_Col': 'New_Col'}, inplace=True)

# Drop columns/rows
df.drop(columns=['col1'], inplace=True)
df.drop(index=0, inplace=True)

df.sort_values(by='Age', ascending=True, inplace=True)  # Sort by column
df.sort_index(inplace=True)                             # Sort by index

# Group and aggregate
grouped = df.groupby('column_name')['value_column'].mean()

# Aggregate multiple metrics
agg = df.groupby('column_name').agg({'col1': 'mean', 'col2': 'sum'})

# Pivot tables
pivot = df.pivot_table(index='column1', columns='column2', values='value', aggfunc='sum')

# Check for missing values
df.isnull().sum()

# Drop rows/columns with missing data
df.dropna(axis=0, inplace=True)        # Drop rows
df.dropna(axis=1, inplace=True)        # Drop columns

# Fill missing data
df.fillna(value=0, inplace=True)       # Fill with a specific value
df['col'].fillna(df['col'].mean(), inplace=True)  # Fill with mean/median

# Merge two DataFrames
merged = pd.merge(df1, df2, on='key_column', how='inner')

# Concatenate DataFrames
concat = pd.concat([df1, df2], axis=0)  # Row-wise
concat = pd.concat([df1, df2], axis=1)  # Column-wise

# Join DataFrames
df1.join(df2, how='left', lsuffix='_left', rsuffix='_right')

df.to_csv('file.csv', index=False)         # Save to CSV
df.to_json('file.json', orient='records')  # Save to JSON

# Unique values
df['col'].unique()                # Get unique values in a column
df['col'].nunique()               # Count unique values in a column

# Value counts
df['col'].value_counts()

# Reset index
df.reset_index(drop=True, inplace=True)

# Check for duplicates
duplicates = df.duplicated()

# Drop duplicates
df.drop_duplicates(inplace=True)
```

### **Datetime Basics**

```python
# Convert to datetime
df['date_col'] = pd.to_datetime(df['date_col'])

# Extract datetime components
df['year'] = df['date_col'].dt.year
df['month'] = df['date_col'].dt.month
df['day'] = df['date_col'].dt.day
df['weekday'] = df['date_col'].dt.day_name()
df['hour'] = df['date_col'].dt.hour

# Check frequency of a datetime index
df.index.freq

# Set column as datetime index
df.set_index('date_col', inplace=True)

# Create a datetime range
date_rng = pd.date_range(start='2025-01-01', end='2025-01-31', freq='D')

# Resample time series data
df.resample('M').sum()          # Resample to monthly and sum
df.resample('W').mean()         # Resample to weekly and calculate mean

# Shift data
df['lagged'] = df['value_col'].shift(1)   # Lag by 1 period
df['lead'] = df['value_col'].shift(-1)    # Lead by 1 period
df['diff'] = df['value_col'].diff()       # First difference

# Generate a time-based range
time_rng = pd.date_range('2025-01-01', periods=10, freq='D')  # Daily
time_rng = pd.date_range('2025-01-01', periods=10, freq='H')  # Hourly
time_rng = pd.date_range('2025-01-01', periods=10, freq='T')  # Minutely

# Resample to different frequencies
df.resample('D').mean()         # Daily mean
df.resample('W').sum()          # Weekly sum
df.resample('M').max()          # Monthly max
df.resample('Q').min()          # Quarterly min

# Rolling window operations
df['rolling_mean'] = df['value_col'].rolling(window=7).mean()  # 7-day rolling mean
df['rolling_sum'] = df['value_col'].rolling(window=7).sum()   # 7-day rolling sum

# Expanding window operations
df['expanding_mean'] = df['value_col'].expanding().mean()     # Expanding mean

# Localize to a timezone
df.index = df.index.tz_localize('UTC')

# Convert to another timezone
df.index = df.index.tz_convert('US/Pacific')

# Filter by date range
df['2025']                      # All rows in 2025
df['2025-01']                   # All rows in January 2025
df.loc['2025-01-01':'2025-01-31']  # Specific date range

# Filter based on day of week
df[df.index.weekday == 0]       # Rows for Mondays

# Basic time series plot
df['value_col'].plot()

# Plot after resampling
df.resample('M')['value_col'].mean().plot()

# Fill missing timestamps in the index
df = df.asfreq('D')             # Daily frequency with missing dates

# Fill missing values
df['value_col'].fillna(method='ffill', inplace=True)  # Forward fill
df['value_col'].fillna(method='bfill', inplace=True)  # Backward fill

# Convert to PeriodIndex for seasonality
df['period'] = df['date_col'].dt.to_period('M')  # Monthly period

# Group by period for analysis
df.groupby(df['date_col'].dt.to_period('M')).sum()
```

### **Method Chaining for Readable and Efficient Code**

```python
# Example of method chaining
result = (
    df
    .set_index('date_col')           # Set datetime column as index
    .resample('M')                   # Resample to monthly frequency
    .agg({'value_col': 'mean'})      # Aggregate with mean
    .rename(columns={'value_col': 'monthly_mean'})  # Rename column
    .reset_index()                   # Reset index to make 'date_col' a column again
)

# Adding new columns using assign
df = (
    df
    .assign(
        year=lambda x: x['date_col'].dt.year,
        month=lambda x: x['date_col'].dt.month,
        day=lambda x: x['date_col'].dt.day
    )
)

# Filtering rows where 'value_col' is greater than 100
filtered_df = df.query('value_col > 100')

# Downcast numerical columns to optimize memory usage
df['value_col'] = pd.to_numeric(df['value_col'], downcast='float')

# Interpolate missing values
df['value_col'] = df['value_col'].interpolate(method='time')
```


