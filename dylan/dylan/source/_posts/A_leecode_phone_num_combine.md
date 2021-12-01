title: A-leecode-手机号T9字母组合
date: 2018-10-10 14:39
category:

- 算法

tags:

- 脑子秀逗
- leecode

------

## 题目解析
>Example:
>Input: "23"
>Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
>Note: Although the above answer is in lexicographical order, your answer could be in any o
<!-- more -->


思路方法和代码演示：
```java
/**
 * Created by dylan on 2018/3/22.
 * 电话号码的组合
 * 分析思路 比如输入123 实际是输入12的结果加上和3对应的组合
 */
public class A17PhoneCombine {

    public List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<String>(); //字母组合结果
        if (digits == null || digits.length() == 0) {
            return result;
        }

        Map<Character, String> dict = new HashMap<Character, String>(); // 初始化拨号T9键盘字典
        dict.put('1', "");
        dict.put('2', "abc");
        dict.put('3', "def");
        dict.put('4', "ghi");
        dict.put('5', "jkl");
        dict.put('6', "mno");
        dict.put('7', "pqrs");
        dict.put('8', "tuv");
        dict.put('9', "wxyz");
        dict.put('0', " ");
        for (char tmp : digits.toCharArray()) {// 循环1
            String val = dict.get(tmp);
            if (val == null) {
                return new ArrayList<String>();

            }
            List<String> tmpArray = new ArrayList<String>();
            for (int i = 0; i < val.length(); i++) {//循环1 的结果result 和 当前tmp数字对应字母组合的处理逻辑
                if (result.size() == 0) {
                    result.add("");
                }
                for (String item : result) {
                    tmpArray.add(item + val.charAt(i));
                }
            }
            result = tmpArray; // 更新当前循环的结果数组
        }
        return result;
    }

    public static void main(String[] args) {
        A17PhoneCombine a17PhoneCombine = new A17PhoneCombine();
        System.out.println(a17PhoneCombine.letterCombinations("123"));


    }
}

```

代码文件：
[A17PhoneCombine.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/apus/A17PhoneCombine.java)

### 总结

- 回溯上次处理结果，类似问题还有排列组合

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
