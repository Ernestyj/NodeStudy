




title: Binary Tree Maximum Path Sum - 二叉树最大路径和
date: 2016-02-12 20:44:47
categories: 
- 算法
tags: 
- java
- 算法
- LeetCode
<!--updated: 2016-02-12 21:40:47-->
---

### Binary Tree Maximum Path Sum - 二叉树最大路径和
**Description**: Given a binary tree, find the maximum path sum. For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path does not need to go through the root.

For example: Given the below binary tree,
    1
  / \\
 2   3
 Return 6.

思路：递归:递归计算左,右子树最大路径和,从左,右子树最大路径和与根节点中选出单侧最大值, 再从单侧最大值,当前全路径和,全局最大路径和中选出最大值.

注意：节点值可能出现负值,比较时不能漏掉单节点情况.

参考：http://www.programcreek.com/2013/02/leetcode-binary-tree-maximum-path-sum-java/

完整的java代码如下：

```java
public class BinaryTreeMaximumPathSum {

    //Definition for a binary tree node.
    public static class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        TreeNode(int x) { val = x; }
    }


    /**
     * http://www.programcreek.com/2013/02/leetcode-binary-tree-maximum-path-sum-java/
     * 递归:递归计算左,右子树最大路径和,从左,右子树最大路径和与根节点中选出单侧最大值,
     再从单侧最大值,当前全路径和,全局最大路径和中选出最大值.
     * 注意节点值可能出现负值,比较时不能漏掉单节点情况.
     */
    private int maxSum = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        maxPath(root);
        return maxSum;
    }
    private int maxPath(TreeNode root) {
        if (root==null) return 0;
        int maxLeft = maxPath(root.left);
        int maxRight = maxPath(root.right);
        //比较root.val, root.val+maxLeft, root.val+maxRight
        int maxSide = Math.max(root.val, Math.max(root.val+maxLeft, root.val+maxRight));
        //比较maxSum, maxCurrent, maxLeft+root.val+maxRight
        maxSum = Math.max(maxSum, Math.max(maxSide, maxLeft+root.val+maxRight));
        return maxSide;
    }

}
```
