title: A02-快速排序
date: 2017-08-12 21:22
category:

- 算法

tags:

- 脑子秀逗
- 排序

------

## 特性
快速排序特点
- 非稳定排序
- 分治模式：那么就存在拆分和组合

<!-- more -->
## 快速排序步骤

- 分治思想，那么源数组每层递归逻辑为：一分为二、对子问题同样方式处理
- 选取枢纽元素（枢纽元素的选取决定有多种快速排序的实现方式）
- 找到枢纽元素在数组中的位置（此处找位置的方法可以多种）
- 对枢纽元素左边，右边做类似处理
- 递归退出，数据已排好序

代码演示：
```java
/**
 * 快速排序， 举例为升序
 *
 * @param a
 * @param m
 * @param n
 */
public static void quickSort(int[] a, int m, int n) {
    if (m < n) {
        int i = m;
        int j = n;
        int pivot = a[m];  // 枢纽元素为当前层级的数据第一个元素
        while (i < j) {
            while (i < j && a[j] > pivot) { // 找到右边第一个小于等于（取决升序还是降序）pivot的位置j，或者i=j
                j--;
            }
            while (i < j && a[i] <= pivot) {// 找到左边第一个大于pivot的位置j，或者i=j。此处=由于选取的m作为枢纽，从m之后开始处理
                i++;
            }
            if (i < j) { // i<j 交换ij位置的值，继续按此方法循环找ij位置
                swap(a, i, j);
            }else if(i==j){ // i=j找到了pivot的位置， 此位置的元素不会大于pivot
                swap(a, m, i);
            }
        } // 以上定位到枢纽元素pivot的索引位置i。找到后固定改位置，对i左边和右边的同样方法处理
        quickSort(a, m, i - 1);
        quickSort(a, i + 1, n);
    }
}

/**
 * 交换函数
 *
 * @param a
 * @param i
 * @param j
 */
private static void swap(int[] a, int i, int j) {
    int tmp = a[i];
    a[i] = a[j];
    a[j] = tmp;
}
```



代码文件：[C7QuickSort.java](https://github.com/yangl326-Dylan/apus/blob/master/src/main/java/com/dylan326/justcode/C7QuickSort.java)

### 总结
- 初始条件
- 选取枢纽元素，找到枢纽元素安置的位置
- 对枢纽元素的前面部分，后面部分分别进行快速排序

------

**版权声明：本文为博主原创文章，未经允许不得转载。**
