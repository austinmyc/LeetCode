
Link to Q: https://leetcode.com/problems/delete-node-in-a-bst/

## Question
Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return _the **root node reference** (possibly updated) of the BST_.

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

## Approach


## Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:
        if not root:
            return None
        #find the node to be deleted
        if key>root.val:
            root.right=self.deleteNode(root.right, key)
        elif key<root.val:
            root.left=self.deleteNode(root.left, key)
        else:
            if not root.right:
                return root.left
            elif not root.left:
                return root.right
            else:
        #replace it with the min val in the right tree / max in the left tree
                cur=root.left
                while cur.right:
                    cur=cur.right
                root.val=cur.val
                root.left=self.deleteNode(root.left, cur.val)
        #recursively delete the copied node
        return root
```
