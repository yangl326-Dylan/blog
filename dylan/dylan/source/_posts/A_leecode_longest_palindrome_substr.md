title: A-leecode-最长回文子串问题
date: 2018-01-29 14:39
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析
>Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.
<!-- more -->



## 分析
1、回文串的定义为字符串为轴对称例如 "aba" "aa" "a" 都可以称为回文串
2、题目找出目标串中最长的回文子串长度

思路方法
### 方法一
首先想到的是穷举法,也是最基本的编码思路的体现。考虑到回文的场景可能为奇数或者偶数场景。
- 回文判定函数[i,j] 判定数组的i到j位回文串
- 从m开始遍历 m ∈ [0,length-1],采用中分方式， 按照奇偶两类情况查找

代码演示：
```java
/**
    * 找所有， 中分方式
    *
    * @param s
    * @return
    */
   public String longestPalindrome(String s) {
       if (s == null) return null;
       if (s.length() == 1) return s;
       char[] array = s.toCharArray();
       if (s.length() == 2) {
           if (array[0] == array[1]) {
               return s;
           } else {
               return s.substring(0, 1);
           }
       }
       int start;
       int end;
       int max = 0;
       int result1 = 0;
       int result2 = 0;

       for (int i = 0; i < array.length; i++) {// 奇数情况
           start = i;
           end = i;
           while (start >= 0 && end < array.length) {
               if (array[start] == array[end]) {
                   if ((end - start + 1) > max) {
                       result1 = start;
                       result2 = end;
                       max = end - start + 1;
                   }
                   start--;
                   end++;
               } else {
                   break;
               }
           }
       }
       for (int i = 0; i < array.length - 1; i++) {//偶数情况
           start = i;
           end = i + 1;
           while (start >= 0 && end < array.length) {
               if (array[start] == array[end]) {
                   if ((end - start + 1) > max) {
                       result1 = start;
                       result2 = end;
                       max = end - start + 1;
                   }
                   start--;
                   end++;
               } else {
                   break;
               }
           }
       }
       return s.substring(result1, result2 + 1);
   }
```

### 方法二
在方法1的穷举法上可以这样思考,最长回文串长度不会超过n（length）, 那么我们可以按照长度n-- 来找。思路较方法1,最坏情况如果长度为1,代价同方法1 全部遍历
- i,i+n-1
- 先找长度为n的回文子串，再找n-1长度的,如果找到了退出查找， 即为结果。

代码演示：略

### 方法三
思考到方法1中其实有很多重复判定,如果知晓r[i+1]\\[j-1]标识数组i+1到j-1位置的子串为回文串,如果a[i] == a[j]条件下 r[i]\\[j]也为回文子串,且长度+2.那么首先想到的就是动态规划,先确定状态转移方程.
需要注意初始条件和遍历条件，这两者取决于转移方程的推导思路.
- a[] 标识原始串数组。r[i]\\[j]标识源串从i到j为回文串
- a[i]=a[j] 并且r[i+1]\\[j-1]为回文串， 那么新结果为i+1,j-1的结果长度+2
- 状态转移方程决定初始条件和遍历条件, 初始条件为a[i]\\[i]=1,遍历条件可以是 i从length-1 开始 i--, j从i+1开始j++.

代码演示：
```java
     /**
     *  方法一  动态规划， result[i][j] 表示 i->j为回文串
     *  那么 array[i]=array[j] 并且result[i+1][j-1]为回文串， 那么新结果为长度+2
     * @param str
     * @return
     */
    public static int maxSubStr(String str) {
        char[] array = str.toCharArray();
        if (array.length <= 1) {
            return array.length;

        }
        int size = array.length;
        int[][] result = new int[size][size];
        int max = 1;
        for (int i = size - 1; i >= 0; i--) { // 注意 遍历的方式和初始条件取决于 状态转移方程。需要利用到之前计算出的结果。
            result[i][i] = 1;
            for (int j = i + 1; j < size; j++) {
                if (array[i] == array[j]) {
                    if (j == i + 1) { // 偶数个数初始场景
                        result[i][j] = 2;
                      } else {
                        if (result[i + 1][j - 1]>0){
                          result[i][j] = result[i + 1][j - 1] + 2;
                        }
                      }
                }
                if (result[i][j] > max) {
                    max = result[i][j];
                    System.out.println(String.format("index,i=%d,j=%d, max=%d", i, j,max));
                }
            }
        }
        return max;
    }
```

### 方法四
回文串特点是反过来也是它本身,那么最长回文子串问题实际就是源串和源串翻转串的最长公共子串问题
但是需要排除掉某些场景"abc123cba"和"abc321cba",可以最长公共子串加上是否回文判定就行
- LCS问题+回文判定

代码演示：

代码文件：
[C9MaxPalindromeSubStr.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/justcode/C9MaxPalindromeSubStr.java)
[C5LCS.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/justcode/C5LCS.java)
[A5LongestPalindromeStr.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A5LongestPalindromeStr.java)

### 总结

- 避免重复计算判定，保存中间结果，符合动态规划条件之一
- 状态转移方程如何推导和编写
- 存在转移关系, 知晓i+1,j-1结果，那么i,j的结果可以推导出来，条件二

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
