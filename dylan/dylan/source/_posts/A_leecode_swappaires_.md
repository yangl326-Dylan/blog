title: A-leecode-单向链表元素两两交换
date: 2019-11-12 16:53
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析

> Given a linked list, swap every two adjacent nodes and return its head.
> Example:
<!-- more -->
> Given 1->2->3->4, you should return the list as 2->1->4->3.
> Note:
> Your algorithm should use only constant extra space.
> You may not modify the values in the list's nodes, only nodes itself may be changed.
> 分析单向链表 需要知道头结点才能做头结点后的节点数据交换（此case是两节点）。
> 实际先交换节点1，2 变成2-1-3-4， 此时2节点为结果的头结点，但是后面的节点没处理
> 然后按照知晓头结点1 处理1-3-4中的3，4 交换， 依次类推处理知道节点后面小于2个节点退出



## 分析
重要点知晓这几类就思路就明白了
1、单向链表仅有一个头结点
2、单向链表的某个节点操作需要知晓它的previous节点

代码演示：
```java
package com.dylan326.apus;

/**
 * Given a linked list, swap every two adjacent nodes and return its head.
 *
 * Example:
 *
 * Given 1->2->3->4, you should return the list as 2->1->4->3.
 * Note:
 *
 * Your algorithm should use only constant extra space.
 * You may not modify the values in the list's nodes, only nodes itself may be changed.
 *
 * 分析单向链表 需要知道头结点才能做头结点后的节点数据交换（此case是两节点）。
 * 实际先交换节点1，2 变成2-1-3-4， 此时2节点为结果的头结点，但是后面的节点没处理
 * 然后按照知晓头结点1 处理1-3-4中的3，4 交换， 依次类推处理知道节点后面小于2个节点退出
 */
public class A24SwapPairs {

    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) { // 初始条件判定
            return head;
        }
        // 首节点交换逻辑 result为结果即头结点， 但是当前后面的数据还没处理
        ListNode result = new ListNode(head.next.val);
        head.next = head.next.next;
        result.next = head;
        ListNode node = head; // 此时2-1-3-4
        while (node.next!=null && node.next.next !=null ){  // 循环退出即后面小于两个节点 不需要做交换
            ListNode tmp1 = node.next; // 处理例子 1-3-4； 1节点后面的数据
            ListNode tmp2 = node.next.next.next;
            node.next = tmp1.next;
            node.next.next = tmp1;
            tmp1.next = tmp2; // 结束后1-4-3

            node = tmp1; // 重置循环初始条件 此时例子应该为 3节点。 如果后面还有数据
        }
        return result;
    }
}

```


代码演示：

代码文件：
[A24SwapPairs.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A24SwapPairs.java)

### 总结
- 实际单向链表的某个节点操作需要什么条件
- 演变问题1: 每三个交换如何处理
- 演变问题2: 比较常见，原链表空间翻转单向链表

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
