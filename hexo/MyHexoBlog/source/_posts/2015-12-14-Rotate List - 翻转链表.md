



title: Rotate List - 翻转链表
date: 2015-12-14 20:44:47
categories: 
- 算法
tags: 
- java
- 算法
- LeetCode
<!--updated: 2015-12-14 21:40:47-->
---

### Rotate List - 翻转链表

**Description**: Given a list, rotate the list to the right by k places, where k is non-negative.
 把后k个rotate到list前面去，k可以超过list本身长度。
 
 For example:
 Given 1->2->3->4->5->NULL and k = 2,
 return 4->5->1->2->3->NULL.

思路：因为k可以超过list本身长度，可以先首尾连起来，然后找到该断开的地方断开。

完整的java代码如下：

```java
public class RotateList {

    public static void main(String[] args) {
        System.out.println("*****RESULT*****");
        System.out.println();
    }


    public static class ListNode {
        int val;
        ListNode next;
        ListNode(int x) { val = x; }
    }


    //因为k可以超过list本身长度，可以先首尾连起来，然后找到该断开的地方断开。
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || k == 0) return head;
        ListNode p = head;
        int len = 1;    //since p is already point to head
        while (p.next != null) {
            len++;
            p = p.next;
        }
        p.next = head;  //form a loop
        k = k % len;
        for (int i = 0; i < len - k; i++) p = p.next;
        //now p points to the prev of the new head
        head = p.next;
        p.next = null;
        return head;
    }

}
```
