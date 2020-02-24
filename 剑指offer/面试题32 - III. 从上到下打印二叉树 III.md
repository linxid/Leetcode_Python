### 题目：
给定一个二叉树，返回其节点值的锯齿形层次遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。
```
例如：
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回锯齿形层次遍历如下：

[
  [3],
  [20,9],
  [15,7]
]
```

### 解析1：
和上一题层次遍历差不多，只是加一个层的判断，奇数和偶数层的处理不同，增加一个判断即可。

* **复杂度：**
|  |复杂度|大小|百分比|
|--|--|--|--|
|时间|$O(n)$|40 ms|97.71%|
|空间|$O(n)$|13.8 MB|5.96%|

```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:return []
        queue = [root]
        level = 0
        res = []
        while queue:
            temp = []
            for _ in range(len(queue)):
                node = queue.pop(0)
                temp.append(node.val)
                if node.left:queue.append(node.left)
                if node.right:queue.append(node.right)
            if level%2 == 0:
                res.append(temp)
            else:
                res.append(temp[::-1])
            level += 1
        return res
```