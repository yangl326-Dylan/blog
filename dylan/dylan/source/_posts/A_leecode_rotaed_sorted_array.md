title: A-leecode-轮转的排序数组查找元素[RotatedSortedArray]
date: 2018-12-24 15:51
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析
> Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
> (i.e., [0,1,2,3,4,5,6] might become [5,6,0,1,2,3,4]).
> You are given a target value to search. If found in the array return its index, otherwise return -1.
> You may assume no duplicate exists in the array.
> Your algorithm's runtime complexity must be in the order of O(log n).
<!-- more -->
> 思路类比二分， 变种，比较中位数和左右两个边界大小， 能确定哪半边是有序，哪半边是转置。再比较大小确target再哪半边，有序的采用二分查找，转置的回到了初始问题


排序数组中超找某个元素，二分查找较快速。 题目有点改动是此排序数组经过轮转， 其实本质还是按照二分查找的思路来

## 分析步骤
1、轮转的递增排序数组，有个特点， 我们取中位数后，必定有一段是单调增，另一段是轮转有序
2、那么就是一个初始条件缩减问题， 如果目标数在单调增里面，那么二分查找，如果不在，回到了1流程初始问题
3、考虑边界条件和循环退出条件

代码演示：
```java
public class A33RotatedSortedArray {

    public int search(int[] nums, int target) {
        int start = 0, end = nums.length - 1;
        if (nums.length == 0) {
            return -1;
        }
        if (target < nums[start] && target > nums[end]) {
            return -1;
        }
        if (target == nums[start] && start == end) {
            return start;
        }
        while (start <= end) {
            int index = (start + end) / 2;
            int tmp = nums[index];
            if (tmp == target) { // 找到目标
                return index;
            }
            if (tmp <= nums[end]) {
                if (target >= tmp && target <= nums[end]) { // target 在有序右侧
                    return searchSecond(nums, target, index, end);
                } else { // target在转置左侧，重新调整右边界
                    end = index - 1;
                }
            } else {
                if (target >= nums[start] && target <= tmp) { // target 在有序左侧
                    return searchSecond(nums, target, start, index);
                } else { //// target在转置左侧，重新调整左边界
                    start = index + 1;
                }
            }
        }
        return -1;
    }

    /**
     * 二分查找
     * @param nums
     * @param target
     * @param start
     * @param end
     * @return
     */
    private static int searchSecond(int[] nums, int target, int start, int end) {
        while (start <= end) {
            if (target < nums[start] || target > nums[end]) {
                return -1;
            }
            int index = (start + end) / 2;
            int tmp = nums[index];
            if (tmp == target) {
                return index;
            }
            if (target < tmp) {
                end = index - 1;
            } else {
                start = index + 1;
            }
        }
        return -1;
    }
```


代码文件：
[A33RotatedSortedArray.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A33RotatedSortedArray.java)

### 总结

- 如果前置条件变化，可能的一种是某些思路的理解演进或者举一反三。 还有一类是思考逻辑递进式

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
