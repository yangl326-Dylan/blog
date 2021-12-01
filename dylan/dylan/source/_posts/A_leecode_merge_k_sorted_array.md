title: A-leecode-合并k个排序数组或链表[Merge k sorted array]
date: 2019-01-09 16:17
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析
>Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.
>合并两数组，归并排序中的一个小步骤。 把这个小步骤演化为合并k个排好序的数组
<!-- more -->


## 分析步骤
1、我们先实现两排序数组或者链表合并， 此为基本编码思路
2、k个参数， 类比归并排序思想，两两合并
3、考察2中的递归逻辑以及递归退出条件

代码演示：
```java
public class A23MergeKSortedList {


    /**
     * 分治+递归
     * @param lists
     * @return
     */
    public ListNode mergeKLists(ListNode[] lists) {

        if (lists.length == 0) {// 边界值， 递归退出条件
            return null;
        } else if (lists.length == 1) {// 边界值， 递归退出条件
            return lists[0];
        } else if (lists.length == 2) {// 边界值， 递归退出条件
            return merge2Lists(lists[0], lists[1]);
        } else {
            ListNode[] params;
            if (lists.length % 2 == 0) { // 偶数个情况
                params = new ListNode[lists.length / 2];
                for (int k = 0; k < params.length; k++) {
                    params[k] = merge2Lists(lists[k], lists[lists.length - k - 1]);
                }
            } else { // 偶数个情况
                params = new ListNode[lists.length / 2 + 1];
                for (int k = 0; k < params.length - 1; k++) {
                    params[k] = merge2Lists(lists[k], lists[lists.length - k - 1]);
                }
                params[params.length - 1] = lists[lists.length / 2];
            }
            return mergeKLists(params); // 递归处理合并
        }

    }

    /**
     * merge2 合并两链表
     * @param list1
     * @param list2
     * @return
     */
    public ListNode merge2Lists(ListNode list1, ListNode list2) {
        ListNode node = new ListNode(0);
        ListNode head = node;
        while (true) {
            if (list1 == null) {
                node.next = list2;
                break;
            }
            if (list2 == null) {
                node.next = list1;
                break;
            }
            if (list1.val == list2.val) {
                node.next = new ListNode(list1.val);
                node.next.next = new ListNode(list1.val);
                node = node.next.next;
                list1 = list1.next;
                list2 = list2.next;
            } else if (list1.val < list2.val) {
                node.next = new ListNode(list1.val);
                list1 = list1.next;
                node = node.next;
            } else {
                node.next = new ListNode(list2.val);
                node = node.next;
                list2 = list2.next;
            }
        }
        return head.next;
    }

    public static void main(String[] args) {
        A23MergeKSortedList tmp = new A23MergeKSortedList();
        ListNode a = new ListNode(1);
        a.next = new ListNode(4);
        a.next.next = new ListNode(5);

        ListNode b = new ListNode(1);
        b.next = new ListNode(3);
        b.next.next = new ListNode(4);

        ListNode c = new ListNode(2);
        c.next = new ListNode(6);

        tmp.mergeKLists(new ListNode[]{a, b, c});
    }
}
```


代码文件：
[A23MergeKSortedList.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A23MergeKSortedList.java)
TODO： 实际解决方案，k个有序联表

### 总结

- 就是和归并排序思想类似
- 方案二，采用K大小的堆去维持合并的数据排序。待续

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
