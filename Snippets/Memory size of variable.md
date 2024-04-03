---
id: Memory size of variable
aliases:
  - probably actually want to
tags: []
---



Find memory size of variable
```python
import sys
sys.getsizeof(x) 

# probably actually want to
df.memory_usage(deep=True)

# or in a Notebook
df.info(memory_usage='deep')
```

