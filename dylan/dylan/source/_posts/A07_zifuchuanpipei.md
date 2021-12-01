title: A07-字符串匹配-KMP
date: 2019-09-18	14:17
category:

- 算法

tags:

- 脑子秀逗
- 数据结构

------
## 单模式串字符串匹配
给定单个字符串S（长度m），查找目标模式串pattern（长度n）。 这个问题常见的会是采用朴素匹配，
<!-- more -->
朴素匹配实际为暴力匹配（BrueForce）本文讲述的是[KMP算法, 维基百科](https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm) 维基百科里面讲述的较详细， 就如下几个重点本文讲述下。

### KMP相对朴素匹配
本质上是在朴素匹配上做了一个剪枝， 朴素匹配在S串上依次对pattern串进行比较,复杂度O(m*n), 而KMP逻辑会进行跳过，复杂度O(m+n)。

### KMP关键点
- 理解字符串的真前缀（proper preffix）、真后缀（proper suffix）。不包含本身的前缀或者后缀，如snake的真前缀s，sn，sna，snak。
- 真前缀和真后缀的相同意味着什么，这个理解清楚了就是KMP对比跳过的剪枝逻辑。理解见代码
- next()函数表及实现
- 根据next()函数遍历目标串S

代码演示：
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class C10StrPattern {

    /**
     * 生成模式串next函数，函数作用为主串对比忽略比较的位置记录
     * 表示的含义当前位置，真前缀和真后缀相同的个数， 正因为相同，所以已经比较过的可以根据这个信息直接跳到比较位置
     * @param pattern 匹配模式串
     * @return
     */
    private static int[] genNextArray(String pattern) {

        if (pattern == null || pattern.length() == 0) {
            return new int[]{};
        }
        int[] result = new int[pattern.length()];
        result[0] = 0;// 一个元素自己，真前、后缀相同个数为0
        for (int i = 1; i < pattern.length(); i++) {
            if (pattern.charAt(i) == pattern.charAt(result[i - 1])) { //当前元素和result记录值
                result[i] = result[i - 1] + 1;
            } else {
                result[i] = 0;
            }

        }
        return result;
    }

    /**
     * @param str
     * @param pattern
     * @return ["1-4","6-9"]
     */
    public static List<String> findPosition(String str, String pattern) {
        List<String> result = new ArrayList<>();
        if (str == null || pattern == null || str.length() == 0 || pattern.length() == 0) { // 不合理过滤
            return result;
        }
        int[] next = genNextArray(pattern); // 生成next函数， 信息表
        int i = 0, start = 0;
        while (i < str.length()) {
            for (int j = 0; j < pattern.length(); j++) {
                if (i + j > str.length() - 1) { // 如果剩下的长度不符合直接退出后续查找
                    return result;
                }
                if (str.charAt(i + j) == pattern.charAt(j)) {
                    if (j == 0) { // j==0 并且i+j位置和 pattern串j位置相等，可能的起始位置记录
                        start = i;
                    }
                    if (j == pattern.length() - 1) {// 找到并且结束
                        result.add(String.format("%s-%s", start, i + j));
                        i++; // **  注意此处从i+1开始继续，而不是当前找到的模式串结束位置
                        break;
                    }
                } else { // ** 不相等 源串遍历索引i 直接跳到next() 位置。 加不加1 取决于next记录值， 有些实现next值默认-1，所以此处不用加1
                    i = i + next[j] + 1;
                    break;
                }
            }

        }

        return result;
    }


    public static void main(String[] args) {
        //示例
        //abababca  原始串S   pattern串aba
        //01234567  索引值
        //00123401  next() 函数，剪枝跳跃的信息表
        System.out.println(Arrays.toString(findPosition("abababca", "aba").toArray()));
    }
}
    

```



代码文件：[C10StrPattern.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/justcode/C10StrPattern.java)

## 总结
- "KMP关键点" 前两点是理解关键，后两点是实现
- AC自动状态机本质来说是KMP的一个多模式演变， 多模串仅一个分支的话就是KMP

机器在于运动，大脑也需要不断思考运作才能避免秀逗

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
