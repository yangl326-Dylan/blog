title: A-leecode-最大容量[MostContainer]
date: 2018-01-14 20:39
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析
>Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn >such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, >such that the container contains the most water.
>Note: You may not slant the container and n is at least 2.
<!-- more -->

给出一系列a(i),任意两个(i, ai) and (i, 0) 和x轴组成的u型矩形面积最大，u型的两边长度可能不一致，所装容量为短板边长决定


## 分析
1、决定u型桶高度的是短板
2、决定面积的是x轴底边和上面所提到的短板边
3、O(n)负复杂度来处理问题，上一情况下，最短边调整，才会可能出现面积较大的场景。 那么采用两边夹逼

代码演示：
```java
/**
 * Created by dylan on 2017/9/21.
 * 两个边的构成一个矩形，为初始面积， 比它面积大的只可能是短边被替换，因为delta X变小，如果出现面积更大，只可能是比短边更长的边
 * 例如图例中最大面积为a2和a4组成的u型矩形 面积为2*2=4
 *               a3  
 *          a2   |    a4
 *     a1   |    |    |
 *     |    |    |    |
 *     ----------------
 */
public class A11MostContainer {
    public int maxArea(int[] height) {
        int max = 0;
        int left = 0;
        int right = height.length - 1;
        while (left <= right) {
            int minHeight = height[left] < height[right] ? height[left] : height[right];//u型桶的短板， 最小竖边
            int curr = (right - left) * minHeight;
            max = max > curr ? max : curr;
            if (height[left] < height[right]) { // 逻辑思路是最短边变化才会出现面积更大的u型桶
                left++;
            } else {
                right--;
            }
        }
        return max;
    }


    public static void main(String[] args) {
      A11MostContainer a11MostContainer = new A11MostContainer();
      System.out.println(a11MostContainer.maxArea(new int[]{1, 2, 3, 2}));
    }
}
```


代码文件：
[A11MostContainer.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A11MostContainer.java)

### 总结

- 如果能想到这个思路，解题较简单， “逻辑思路是最短边变化才会出现面积更大的u型桶”。

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
