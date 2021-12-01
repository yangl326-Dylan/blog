title: A-leecode-和为目标值问题
date: 2019-06-26 16:18
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析
>Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.
>The same repeated number may be chosen from candidates unlimited number of times.
<!-- more -->



## 分析
1、这类问题其实条件较重要，候选数字无重复、目标结果唯一

思路方法
### 方法一
这类问题递归（回溯）去处理只需要明确递归函数参数定义和含义，其实问题就解决了一大半了
- 详见代码参数注释

代码演示：
```java
package com.dylan326.apus;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

/**
 * 条件都是正数，backtracking 模式， 之前的三数和或者三数靠近和， 回溯模式也能解决
 * 回溯解决的一类问题
 */
public class A39combinationSum {

    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> list = new ArrayList<List<Integer>>();
        backtrack(list, new ArrayList<Integer>(), candidates, target, 0);
        return list;
    }

    /**
     *
     * @param list 结果集合
     * @param tempList 结果
     * @param nums 候选数组
     * @param remain 目标值在当前循环或者递归剩下值，当前题目及target（上次的remain-nums[i]）
     * @param start 回溯开始的起始位置
     */
    private void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums, int remain, int start) {
        if (remain < 0) {
            System.out.println("-----illegal="+Arrays.toString(tempList.toArray()));
            return;
        }
        else if (remain == 0) { // 结果条件
            System.out.println("found="+Arrays.toString(tempList.toArray()));
            list.add(new ArrayList<>(tempList)); //  新数组对象保留结果
        } else {
            for (int i = start; i < nums.length; i++) {
                tempList.add(nums[i]);
                System.out.println("=add="+nums[i]+",array="+Arrays.toString(tempList.toArray()));
//                backtrack(list, tempList, nums, remain - nums[i], i + 1);// start 参数取决于包不包含自己
                backtrack(list, tempList, nums, remain - nums[i], i);// 回溯开始位置从当前元素开始
                tempList.remove(tempList.size() - 1);
            }
        }
    }

    public static void main(String[] args) {
        A39combinationSum a39combinationSum = new A39combinationSum();
        System.out.println(Arrays.toString(a39combinationSum.combinationSum(new int[]{7, 2, 3, 4}, 7).toArray()));
    }
}

```


代码演示：见 A39combinationSum.java

代码文件：
[A39combinationSum.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A39combinationSum.java)

### 总结

- 退出递归条件、或者找到结果条件
- 实际为递归全组合的一种剪枝方式

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
