title: A-leecode-反转整数[ReverseInteger]
date: 2018-09-03 17:39
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析
>Given a 32-bit signed integer, reverse digits of an integer.
>''' example: 1234->4321
>'''
<!-- more -->

反转一个整数

## 分析步骤
1、整数的反转比起字符串因为整数的特性，思路少许不一样

代码演示：
```java
/**
 * Created by dylan on 2017/5/22.
 * 翻转整数和翻转数据串可以用不一样的思路， 因为整数的特性
 */
public class A7ReverseInteger {
    public int reverse(int x) {
        long i = 0; // 注意整数反转可能越界
        while (x != 0) {
            i = i * 10 + x % 10; // 末尾进位
            x = x / 10; //移除掉末尾
        }
        if (i > Integer.MAX_VALUE || i < Integer.MIN_VALUE) {
            i = 0;
        }
        return (int) i;
    }
}

```


代码文件：
[A7ReverseInteger.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A7ReverseInteger.java)

### 总结

- 主要是每次余数作为高位，性能可以再考虑下

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
