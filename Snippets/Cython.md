
```python
%load_ext Cython
```

```python
%%cython
import random
import numpy as np
def between_cy3(x: np.int64, y: np.int64) -> np.int64:
	return random.randint(x, y)
```

```python
(df
.str.split('-', expand=True)
.astype(int)
 .apply(lambda row: between_cy3(row[0], row[1]), axis=1)
)
```

