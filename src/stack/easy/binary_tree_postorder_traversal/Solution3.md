> 方法3：Morris 遍历

**Morris 遍历思路与算法**

有一种巧妙的方法可以在线性时间内，只占用常数空间来实现后序遍历。这种方法由 J. H. Morris 在 1979 年的论文「Traversing Binary Trees Simply and Cheaply」中首次提出，因此被称为 Morris 遍历。

Morris 遍历的核心思想是利用树的大量空闲指针，实现空间开销的极限缩减。其后序遍历规则总结如下：

新建临时节点，令该节点为 root；

如果当前节点的左子节点为空，则遍历当前节点的右子节点；

如果当前节点的左子节点不为空，在当前节点的左子树中找到当前节点在中序遍历下的前驱节点；

如果前驱节点的右子节点为空，将前驱节点的右子节点设置为当前节点，当前节点更新为当前节点的左子节点。

如果前驱节点的右子节点为当前节点，将它的右子节点重新设为空。倒序输出从当前节点的左子节点到该前驱节点这条路径上的所有节点。当前节点更新为当前节点的右子节点。

重复步骤 2 和步骤 3，直到遍历结束。

参考代码：

```java
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<Integer>();
    if (root == null) {
        return res;
    }

    TreeNode p1 = root, p2 = null;

    while (p1 != null) {
        p2 = p1.left;
        if (p2 != null) {
            while (p2.right != null && p2.right != p1) {
                p2 = p2.right;
            }
            if (p2.right == null) {
                p2.right = p1;
                p1 = p1.left;
                continue;
            } else {
                p2.right = null;
                addPath(res, p1.left);
            }
        }
        p1 = p1.right;
    }
    addPath(res, root);
    return res;
}

public void addPath(List<Integer> res, TreeNode node) {
    int count = 0;
    while (node != null) {
        ++count;
        res.add(node.val);
        node = node.right;
    }
    int left = res.size() - count, right = res.size() - 1;
    while (left < right) {
        int temp = res.get(left);
        res.set(left, res.get(right));
        res.set(right, temp);
        left++;
        right--;
    }
}
```

