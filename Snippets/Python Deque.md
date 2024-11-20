
```python
from collections import deque

# Create a deque
d = deque([1, 2, 3])

# Append to both ends
d.append(4)          # [1, 2, 3, 4]
d.appendleft(0)      # [0, 1, 2, 3, 4]

# Pop from both ends
d.pop()              # [0, 1, 2, 3]
d.popleft()          # [1, 2, 3]

# Extend and extendleft
d.extend([5, 6])     # [1, 2, 3, 5, 6]
d.extendleft([-1, -2])  # [-2, -1, 1, 2, 3, 5, 6]

# Rotate
d.rotate(2)          # [5, 6, -2, -1, 1, 2, 3]
d.rotate(-3)         # [-1, 1, 2, 3, 5, 6, -2]

# Remove and count
d.remove(2)          # [-1, 1, 3, 5, 6, -2]
count = d.count(1)   # 1
```
