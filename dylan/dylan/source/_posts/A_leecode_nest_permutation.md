title: A-leecode-字典序下一个[NextPermutation]
date: 2018-11-26 14:22
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析
>Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.
>If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).
>The replacement must be in-place and use only constant extra memory.
>Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.
<!-- more -->
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1


## 分析步骤
关键要点
1、左领位小的第一的数n，例子（4、5、3、2）依次是2，3，5，4 那么n=4
2、找到4的右边比n=4大的最小的一个数，例子是5。 交换这两个数字
3、n=4右边的数据排序为递增序列， 即从小到大排序 5、2、3、4

代码演示：
```java
/**
 * Created by dylan on 2017/5/22.
 * 字典序的下一个数字, 如果没有则为原数组
 * 1,4,3,2 -> 2,1,3,4
 * 1,3,4,2 -> 1,4,2,3
 */
public class A31NextPermutation {

    public static int[] next(int[] nums) {
        int tmp1 = -1;
        int index1 = 0;
        for (int i = nums.length - 1; i > 0; i--) {//记录从右边开始查找，找到的第一个左邻位小的数
            if (nums[i - 1] < nums[i]) {
                tmp1 = nums[i - 1];
                index1 = i - 1;
                break;
            }
        }
        if (tmp1 == -1) { // 找不到则为字典序的最大值， 下一个按照题要求为回到最小值
//            return num;
            int m = 0, n = nums.length - 1;
            while (m < n) {
                int tmp = nums[m];
                nums[m++] = nums[n];
                nums[n--] = tmp;
            }
            return nums;
        }
        int delta = Integer.MAX_VALUE;
        int index2 = 0;
        for (int i = index1 + 1; i < nums.length; i++) {//找到比tmp1大的最小数
            if (nums[i] > tmp1 && nums[i] - tmp1 < delta) {
                delta = nums[i] - tmp1;
                index2 = i;

            }
        }
        //swap
        nums[index1] = nums[index2];
        nums[index2] = tmp1;

        //sort index1+1~ num.lengh
        for (int i = index1 + 1; i < nums.length; i++) {// 对index1后面的数据按小到大排序
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] > nums[j]) {
                    int tmp = nums[i];
                    nums[i] = nums[j];
                    nums[j] = tmp;
                }
            }
        }
        return nums;
    }
}
```


代码文件：
[A31NextPermutation.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A31NextPermutation.java)

### 总结

- 定义的实现过程，如何把理解的定义程序化编写出来

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
