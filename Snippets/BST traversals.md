
```python
def inorder_traversal(root):
    if root is None:
        return []
    return (inorder_traversal(root.left)
	 + [root.val] 
	 + inorder_traversal(root.right))
```

