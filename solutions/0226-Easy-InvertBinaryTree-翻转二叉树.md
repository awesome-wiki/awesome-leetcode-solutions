# [226-翻转二叉树/Invert Binary Tree](https://leetcode-cn.com/problems/invert-binary-tree)

## Problems

[226-翻转二叉树/Invert Binary Tree](https://leetcode-cn.com/problems/invert-binary-tree)

### CN

翻转一棵二叉树。

示例：

输入：
```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

输出：

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

### EN

Invert a binary tree.

Example:

Input:
```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

Output:
```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

## 解法

官方题解：[leetcode-cn/反转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/solution/fan-zhuan-er-cha-shu-by-leetcode/)

### 解法一：递归

思路：采用递归的思想解决的，依旧是要用「自上而下」的方式思考问题。

Java：

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    //  自定向下的思考方式
    //  递归
    // invert(root) = invert(root->left) + invert(root->right)
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        // https://www.jianshu.com/p/b2d2edb4ba5b
        TreeNode left = invertTree(root.left);
        TreeNode right = invertTree(root.right);
        root.left = right;
        root.right = left;
        return root;
    }
}
```