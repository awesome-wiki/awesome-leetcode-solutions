# [24 Swap Nodes in Pairs/两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

## 题目

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

实例 1：

![示例](https://gitee.com/michael_xiang/images/raw/master/uPic/jJxRpJ.png)

```
输入：head = [1,2,3,4]
输出：[2,1,4,3]
```

示例 2：
```
输入：head = []
输出：[]
```

示例 3：
```
输入：head = [1]
输出：[1]
```
## 题解

### 递归

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode next = head.next;
        head.next = swapPairs(next.next);
        next.next = head;
        return next;
    }
}
```

总结：这道题利用递归的解法来做，确实可以减小考虑的复杂度。关键点是要找到正确的终止条件。看题解非常简单，但是为何却划分为 Medium，因为解这道题需要链表的前置知识。