title: A-leecode-两排序数组的中位数
date: 2018-03-22 11:39
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析
>给出两个排好序的数组，找出合并后的中位数。很基础，组合排序的中间流程，我面试候选者有时会考察这个题目
<!-- more -->



## 分析和思路方法
1、中位数为奇偶两类场景
2、输入两数组已排好序， 找到合并后（m+n）/2 或者 （m+n+1）/2 位置的数。 但是不需要使用合并新空间
3、两个数组同时遍历 查找其M=（m+n）/2 或者 （m+n+1）/2位置的数


代码演示：
```java
/**
 * 很基础，组合排序的中间流程，我面试候选者有时会考察这个题目
 * 注意代码段和方法拆分， 这样可读性更强
 */
public class A4MedianOfTwoSortedArray {
    public static double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int la = nums1.length;
        int lb = nums2.length;
        if (la == lb && lb == 0) {
            return 0;
        }
        if ((la + lb) % 2 == 0) {
            int m1 = (la + lb) / 2;
            int m2 = m1 + 1;
            return (findM(nums1, nums2, m1) + findM(nums1, nums2, m2)) * 1.0 / 2.0;
        } else {
            return findM(nums1, nums2, (la + lb + 1) / 2);
        }
    }

    /**
     * size(a) >size(b)
     *
     * @param a
     * @param b
     * @param m m<=size(a+b)
     * @return
     */
    private static int findM(int[] a, int[] b, int m) {
        int la = a.length;
        int lb = b.length;
        int counter = 0;
        int t1 = 0, t2 = 0;
        int result;
        while (true) {
            if (t1 == la) {
                result = b[t2];
                t2++;
            } else if (t2 == lb) {
                result = a[t1];
                t1++;
            } else if (a[t1] <= b[t2]) {
                result = a[t1];
                t1++;
            } else {
                result = b[t2];
                t2++;
            }
            counter++;
            if (counter == m) break;
        }
        return result;
    }

    public static void main(String[] args) {
        System.out.println(findMedianSortedArrays(new int[]{1, 3, 5, 6}, new int[]{2, 7, 9, 10}));
    }
```


代码文件：
[A4MedianOfTwoSortedArray.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A4MedianOfTwoSortedArray.java)

### 总结

- 无他，良好习惯，代码片段方法抽离

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
