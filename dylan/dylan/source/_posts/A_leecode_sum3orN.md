title: A-leecode-三数和[Three Sum] or N数和或者相近
date: 2019-01-28 15:01
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析
>Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.
>Note:
> The solution set must not contain duplicate triplets.
<!-- more -->



## 分析步骤
1、条件给出子元素三个和为0
2、限制和前置条件， 非重复数组
3、思路：最直接的思路未尝不好， 限制仅为3数

代码演示：
```java
public class A15Sum3 {

    /**
     * 直接处理方式
     *
     * @param nums
     * @param target
     * @return
     */
    public static List<List<Integer>> sum3(int[] nums, int target) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (nums.length < 3) { // 初始条件检查
            return result;
        }
        Arrays.sort(nums); // 排好序
        for (int i = 0; i < nums.length; i++) {
            int start = i + 1, end = nums.length - 1;
            int tmp = target - nums[i];
            if (i > 0 && nums[i] == nums[i - 1]) { // 相等元素 继续下一个
                continue;
            }
            while (start < end) {
                if (tmp < nums[start] + nums[end]) {
                    end--;
                } else if (tmp > nums[start] + nums[end]) {
                    start++;
                } else {
                    List<Integer> tmp2 = new ArrayList<Integer>();
                    tmp2.add(nums[i]);
                    tmp2.add(nums[start]);
                    tmp2.add(nums[end]);
                    start++;
                    end--;
                    while (start < end && nums[start] == nums[start - 1]) {
                        start++;
                    }
                    while (end > start && nums[end] == nums[end + 1]) {
                        end--;
                    }
                    result.add(tmp2);
                }
            }


        }
        return result;
    }

    /**
     * N数和或者和靠近处理模式
     *
     * @param nums
     * @param target
     * @return
     */
    public static List<List<Integer>> sum3New(int[] nums, int target) {
        Map<List<Integer>, List<Integer>> result = new HashMap<>();
        Arrays.sort(nums);
        sum3Backtracking(result, new ArrayList<Integer>(), nums, target, 0);
        return new ArrayList<>(result.values());
    }

    /**
     * backtracking 来处理
     *
     * @param result
     * @param item
     * @param nums
     * @param remain
     * @param start
     */
    public static void sum3Backtracking(Map<List<Integer>, List<Integer>> result, List<Integer> item, int[] nums, int remain, int start) {
        if (nums.length> 0 && remain < minArraySum(nums)) {
            return;
        } else if (remain == 0 && item.size() == 3) { // 符合结果值
            result.put(new ArrayList<>(item), new ArrayList<>(item)); // 按照题目要求，简单用hashmap去重复数组
        } else {
            for (int i = start; i < nums.length; i++) {
                item.add(nums[i]);//* ① 添加当前元素
                sum3Backtracking(result, item, nums, remain - nums[i], i + 1); //* ② 之前的目标值为remain-nums[i]
                item.remove(item.size() - 1); // * ③ 回退元素
            }
        }
    }

    /**
     * 计算出当前最小值， 退出递归的条件，减少递归次数
     * @param nums
     * @return
     */
    private static int minArraySum(int[] nums) {
        int start = 0;
        if (start >= nums.length) {
            return Integer.MAX_VALUE;
        }
        if (nums[start] >= 0) {
            return nums[start];
        } else {
            int min = 0;
            for (int i = start; i < nums.length; i++) {
                if (nums[i] < 0 && i < 4) {
                    min += nums[i];
                }
            }
            return min;
        }
    }


    public static void main(String[] args) {
        System.out.println(sum3(new int[]{0, 0, 0, 0, 0, 0}, 0));
        System.out.println(sum3New(new int[]{0, 0, 0, 0, 0, 0}, 0));
        //
        System.out.println(sum3(new int[]{-2, -1, 0, 1, 2, 3}, 0));
        System.out.println(sum3New(new int[]{-2, -1, 0, 1, 2, 3}, 0));
    }
}
```


代码文件：
[A15Sum3.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A15Sum3.java)

### 总结

- 首先相当的类似回溯处理， 需要解决的是重复数组结果问题
- 直接处理方式， 避免了重复检查， 当限制进位3数和，可以直接考虑
- 延伸问题： N数和 或者 N数和接近，这类仅是结束条件变更的扩展

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
