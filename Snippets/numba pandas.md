
```python
import numba as nb
import numpy as np

@nb.jit(nb.int32[:](nb.int32[:], nb.int32[:]))
def between_nb(arr1, arr2):
	return np.random.randint(arr1, arr2)
```


