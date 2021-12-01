title: A-leecode-两数和[Two Sum]
date: 2017-09-22 20:39
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析
>Given an array of integers, return indices of the two numbers such that they add up to a specific target.
>You may assume that each input would have exactly one solution, and you may not use the same element twice.
>''' example:
>Given nums = [2, 7, 11, 15], target = 9,
>Because nums[0] + nums[1] = 2 + 7 = 9,
>return [0, 1].
>'''
<!-- more -->

整型数组中，找出两个数（不能是同一个元素），满足他们的和是给定的target值。 假设有唯一一组解。
这个假设简化了结果输出条件，和代码边界逻辑。 实际问题中记住尽可能的去考虑这些条件和情况。

## 分析步骤
1、直接给出两数的所有和，和目标值相等的返回这两个数的索引值
2、步骤1太直接了， 大部分人都这样说。 但我们为什么不能先写出来，再分析问题点， 可以从哪些方面去优化处理
3、实现和分析见code

代码演示：
```java
public class A1Sum2 {

    /**
     * 直接思路方法
     * @param nums
     * @param target
     * @return
     */
    public static int[] a1Sum2Method1(int[] nums, int target) {
        int[] result = new int[]{0, 0};
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if ((nums[i] + nums[j]) == target) {
                    result[0] = i;
                    result[1] = j;
                    return result;
                }
            }
        }
        return result;
    }


    public static int[] a1Sum2Method2(int[] nums, int target) {
        int[] result = new int[]{0, 0};
        Map<Integer, Integer> tmp = new HashMap();
        for (int i = 0; i < nums.length; i++) { // 空间换时间。存储值和索引对应关系
            tmp.put(nums[i], i);
        }

        for (int i = 0; i < nums.length - 1; i++) {
            Integer j = tmp.get(target - nums[i]);
            if (j != null && j != i) { // 去除掉 自己的判定
                result[0] = i;
                result[1] = j;
            }
        }
        return result;
    }

    public static void main(String[] args) {
        System.out.println(Arrays.toString(a1Sum2Method1(new int[]{2, 3, 5}, 5)));
        System.out.println(Arrays.toString(a1Sum2Method2(new int[]{2, 3, 5}, 5)));
    }
}

```


代码文件：
[A1Sum2.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A1Sum2.java)

### 总结

- 有些问题在条件容许的情况下可以思考出直接的方式，
- 空间换取时间问题：类似如 整型数据数组中连续子串求和为指定值的个数等

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
