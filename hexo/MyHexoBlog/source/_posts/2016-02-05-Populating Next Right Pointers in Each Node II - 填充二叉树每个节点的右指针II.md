




title: Populating Next Right Pointers in Each Node II - 填充二叉树每个节点的右指针II
date: 2016-02-05 20:44:47
categories: 
- 算法
tags: 
- java
- 算法
- LeetCode
<!--updated: 2016-02-05 21:40:47-->
---

### Populating Next Right Pointers in Each Node II - 填充二叉树每个节点的右指针II
**Description**: Follow up for problem "Populating Next Right Pointers in Each Node". What if the given tree could be any binary tree? Would your previous solution still work?

Note: You may only use constant extra space.

 思路：
 1 找到规律用递归求解,类似上一题Populating Next Right Pointers in Each Node, 唯一的不同是每次要先找到一个第一个有效的next链接节点，并且递归的时候要先处理右子树，再处理左子树.（(OJ 78%，思路较难想到）
 参考：http://fisherlei.blogspot.tw/2012/12/leetcode-populating-next-right-pointers_29.html
2 类似二叉树层次遍历,但不再使用队列,而是将树的每一层维护成一个链表,空间复杂度O(1); 每次维护两层,共计4个指针:lastHead, curHead, lastCur, curPre.
参考：http://www.programcreek.com/2014/06/leetcode-populating-next-right-pointers-in-each-node-ii-java/
3 类似二叉树层次遍历,使用队列,空间复杂度O(n)

完整的java代码如下（含三种方法）：

```java
public class PopulatingNextRightPointersInEachNodeII {

    public static class TreeLinkNode {
        int val;
        TreeLinkNode left, right, next;
        TreeLinkNode(int x) { val = x; }
    }

    /**(OJ 78%)
     * http://fisherlei.blogspot.tw/2012/12/leetcode-populating-next-right-pointers_29.html
     * 找到规律用递归求解,类似上一题Populating Next Right Pointers in Each Node,
     唯一的不同是每次要先找到一个第一个有效的next链接节点，并且递归的时候要先处理右子树，再处理左子树.
     空间复杂度O(1)
     * @param root
     */
    public void connect(TreeLinkNode root) {
        if (root==null) return;
        TreeLinkNode p = root.next;
        while (p!=null){
            if (p.left!=null) {
                p = p.left; break;
            }
            if (p.right!=null) {
                p = p.right; break;
            }
            p = p.next;
        }
        if (root.right!=null) root.right.next = p;
        if (root.left!=null) root.left.next = root.right!=null ? root.right : p;
        connect(root.right);
        connect(root.left);
    }

    /**(OJ 30%)
     * http://www.programcreek.com/2014/06/leetcode-populating-next-right-pointers-in-each-node-ii-java/
     * 类似二叉树层次遍历,但不再使用队列,而是将树的每一层维护成一个链表,空间复杂度O(1);
     每次维护两层,共计4个指针:lastHead, curHead, lastCur, curPre.
     * @param root
     */
    public void connect1(TreeLinkNode root) {
        if(root == null) return;
        TreeLinkNode lastHead = root;
        TreeLinkNode curHead = null;
        TreeLinkNode lastCur = null;
        TreeLinkNode curPre = null;
        while(lastHead!=null) {
            lastCur = lastHead;
            while(lastCur != null) {
                if(lastCur.left!=null) {
                    if(curHead == null) {
                        curHead = lastCur.left;
                        curPre = lastCur.left;
                    } else {
                        curPre.next = lastCur.left;
                        curPre = curPre.next;
                    }
                }
                if(lastCur.right!=null) {
                    if(curHead == null) {
                        curHead = lastCur.right;
                        curPre = lastCur.right;
                    } else {
                        curPre.next = lastCur.right;
                        curPre = curPre.next;
                    }
                }
                lastCur = lastCur.next;
            }
            lastHead = curHead; //往下层移动
            curHead = null;
        }
    }

    /**类似二叉树层次遍历,使用队列,空间复杂度O(n)
     * @param root
     */
    public void connect2(TreeLinkNode root) {
        if (root==null) return;
        Queue<TreeLinkNode> curQueue = new LinkedList<>();
        Queue<TreeLinkNode> nextQueue = new LinkedList<>();
        curQueue.offer(root);
        TreeLinkNode old = null;
        while (!curQueue.isEmpty()){
            TreeLinkNode node = curQueue.poll();
            if (old!=null) old.next = node;
            old = node;
            if (node.left!=null) nextQueue.offer(node.left);
            if (node.right!=null) nextQueue.offer(node.right);
            if (curQueue.isEmpty()){
                old = null;
                curQueue = nextQueue;
                nextQueue = new LinkedList<>();
            }
        }
    }

}
```
