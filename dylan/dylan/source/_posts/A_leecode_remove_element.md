title: A-leecode-移除元素[remove element]
date: 2018-10-30 14:56
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析
>Given an array nums and a value val, remove all instances of that value in-place and return the new length.
>Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
>The order of elements can be changed. It doesn't matter what you leave beyond the new length.
>Example 1:
>Given nums = [3,2,2,3], val = 3,
>Your function should return length = 2, with the first two elements of nums being 2.
>It doesn't matter what you leave beyond the returned length.
<!-- more -->

整型数组中移除和目标val相同的元素，返回剩下数据的长度n，数组前n元素是结果元素

## 分析步骤
1、返回非val元素个数n，并且数组前n是非val 元素， 注意顺序无要求
2、除去n个元素外剩余的元素内容也没要求
3、不开辟额外的数组空间

代码演示：
```java
/**
 * Given an array nums and a value val, remove all instances of that value in-place and return the new length.
 *
 * Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
 *
 * The order of elements can be changed. It doesn't matter what you leave beyond the new length.
 * 分析 ：直接方案是遍历数组 遇到和val相同的元素 与后面不和val相同的元素交换
 * 此处小技巧， 后面不同于val的元素可以按照倒序来交换
 * 实现相对较OK  优于99.85%的提交
 */
public class A27RemoveElement {

    public int removeElement(int[] nums, int val) {
        int counter = 0;
        int end = nums.length - 1; // end标记需要交换的元素
        for (int i = 0; i < nums.length; i++) {
            if(i > end) break;
            if(nums[i] == val){
                while (nums[end]==val){// 从尾部向前找 第一个不等于val的元素
                    end--;
                    if(end <i){ // 全部是val的情况会导致end < 此时i的值， 返回统计计数
                        return counter;
                    }
                }
                int tmp = nums[i]; // 交换i和end元素位置
                nums[i] = nums[end];
                nums[end] = tmp;
                end--;
                counter++; // 和不同于val的元素交换后需要计数++
            } else {
                counter++; // 不同于val的元素 计数++
            }
        }
        return counter;
    }

    public static void main(String[] args) {
        A27RemoveElement a= new A27RemoveElement();
        a.removeElement(new int[]{4,5},5);

    }
}
```


代码文件：
[A27RemoveElement.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A27RemoveElement.java)

### 总结

- 顺序思路实现，优化了下小细节， 主要还是防脑袋秀逗。 思考思考，写写

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
