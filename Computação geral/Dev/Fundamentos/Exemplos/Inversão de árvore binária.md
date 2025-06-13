```python
class Solution:
	def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]
		def invert(root):
			if not root:
				return
			root.left, root.right = root.right, root.left
			invert(root.left)
			invert(root.right)
			
		invert(root)
		return root
```

---

> [!NOTE] Referências
> - [Youtube@Augusto Galego](https://www.youtube.com/watch?v=-KHB9frk6vk)
