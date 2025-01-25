
```python
def preorder_traversal(root):
    if root is None:
        return []
    return ([root.val] 
        + preorder_traversal(root.left) 
        + preorder_traversal(root.right))
```


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


```python
class Solution:
    def areValuesSame(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> bool:
        # Helper function to perform in-order traversal iteratively
        def inOrderIterator(root):
            stack = []
            current = root
            while stack or current:
                while current:
                    stack.append(current)
                    current = current.left
                current = stack.pop()
                yield current.val  # Yield the current value
                current = current.right

        # Initialize in-order iterators for both trees
        iter1 = inOrderIterator(root1)
        iter2 = inOrderIterator(root2)

        # Compare values from both iterators
        while True:
            try:
                val1 = next(iter1)
            except StopIteration:
                val1 = None  # No more nodes in tree 1

            try:
                val2 = next(iter2)
            except StopIteration:
                val2 = None  # No more nodes in tree 2

            # If one tree ends before the other or values differ
            if val1 != val2:
                return False

            # If both trees are exhausted
            if val1 is None and val2 is None:
                return True

```

