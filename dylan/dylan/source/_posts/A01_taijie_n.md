title: A01-递归式-台阶走法
date: 2017-07-22 21:30
category:

- 算法

tags:

- 脑子秀逗
- 递归

---
问题
>n个台阶走法问题， 已知可以一次一个台阶，一次两个台阶，一次三个台阶。 那么n个台阶有多少种走法？

问题分析步骤
1. n个台阶的走法为n-1个台阶走法+1，1=走一个台阶
2. 最后一步的走法可以是题目中的三类
3. 那么最后的结果必然是，最后的方案是一步、两步、或者三步，走法的和即为结果
4. 最小边界， 只有一个台阶，两个台阶，三个台阶

```java
public static int nTJ(int n) {
        if (n == 1) {
            return 1;
        }
        if (n == 2) {
            return 2;
        }
        if (n == 3) {
            return 4;
        }
        if (n > 3) {
            return nTJ(n - 1) + nTJ(n - 2) + nTJ(n - 3);
        }
        return 0;
}
```

代码:[C6nTJ.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/justcode/C6nTJ.java)

---

**版权声明：本文为博主原创文章，未经允许不得转载。**
