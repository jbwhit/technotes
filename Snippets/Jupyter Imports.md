
```python
%load_ext autoreload
%autoreload 1
%config InlineBackend.figure_format = 'retina'
%load_ext rich
import datetime
import hashlib
import json
import os
import re
import sys
import time
import warnings

import ipywidgets as widgets
import matplotlib as mpl
import matplotlib.pyplot as plt
import numpy as np
import pyarrow as pa
import pandas as pd
import requests
import seaborn as sns
from IPython.display import Markdown, display
from matplotlib.ticker import FuncFormatter
from pandas.plotting import register_matplotlib_converters
from scipy.stats import norm
from ydata_profiling import ProfileReport

from sklearn import set_config
set_config(transform_output='pandas')

register_matplotlib_converters()
sns.set()
sns.set_context("notebook")
plt.rcParams["figure.figsize"] = 10, 6

# To see all columns (don't truncate wide DataFrames)
pd.set_option('display.max_columns', None) 
# To see all rows (don't truncate long DataFrames) 
pd.set_option('display.max_rows', None) 

# To reset to default settings if needed pd.reset_option('display.max_columns') 
pd.reset_option('display.max_rows') # You can also set the width of the display 
pd.set_option('display.width', None)

pd.options.display.precision = 4
warnings.simplefilter(action="ignore", category=FutureWarning)

dollar_formatter = FuncFormatter(lambda x, pos: f"${x:,.0f}")
thousands_formatter = FuncFormatter(lambda x, pos: f"{x:,.0f}")

string_pa = pd.ArrowDtype(pa.string()) # alias from Effective Pandas 2

```



## Examples


```python
ex = pd.Series(text_var, dtype=string_pa)
```