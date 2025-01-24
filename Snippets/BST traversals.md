
```python
def inorder_traversal(root):
    if root is None:
        return []
    return (inorder_traversal(root.left)
	 + [root.val] 
	 + inorder_traversal(root.right))
```

```python
def postorder_traversal(root):
    if root is None:
        return []
    return (postorder_traversal(root.left) 
        + postorder_traversal(root.right) 
        + [root.val])
```

```python
from collections import deque

def level_order_traversal(root):
    if root is None:
        return []
    
    result = []
    queue = deque([root])
    
    while queue:
        node = queue.popleft()
        result.append(node.val)
        
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)
    
    return result

```