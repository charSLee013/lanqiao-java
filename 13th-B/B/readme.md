##【问题描述】 
这天小明正在学数数。他突然发现有些正整数的形状像一座“山”，比如 123565321 、 145541 ，它们左右对称（回文）且数位上的数字先单调不减，后单调不增。小明数了很久也没有数完，他想让你告诉他在区间 `[2022,2022222022]` 中有多少个数的形状像一座“山”。

## 解题思路
---

### 暴力推算
将数字转换成 `String` 类型
然后使用字符串回文检查方法的来检查
再设置一个`max`的int，用来检查规则中单调递增或者不增的规则

```java
class Main{
    public static void main(String[] args) {
        int count = 0;
        for(int i = 2022;i <= 2022222022;i++){
            String s = String.valueOf(i);
            int len = s.length();
            int max = -1;

            boolean sign = true;
            for(int j = 0; j < len/2;j++){
                if(s.charAt(j) != s.charAt(len-j-1)){
                    sign  =false;
                    break;
                }

                if(s.charAt(j) > s.charAt(j+1)){
                    sign = false;
                    break;
                }
            }

            if(sign) count++;
        }

        System.out.println(count);
    }
}
```

### 数字反转
数字反转是一种常见的数学技巧，用于将整数的数字顺序反向。在计算机科学中，数字反转经常被用于字符串、数字等类型的操作中，例如判断一个整数是否为回文数、计算一个数字的位数以及反转字符串等操作。

数字反转的实现方式是通过使用模除和整除运算来获取整数的各个位数，并使用乘法和加法操作将它们组合成一个新的整数。下面是一个示例实现：
```java
public static int reverseNumber(int num) {
    int reverseNum = 0;
    while (num > 0) {
        int digit = num % 10; // 获取个位上的数字
        reverseNum = reverseNum * 10 + digit; // 将数字放置到最高位
        num /= 10; // 移除已经处理过的最低位
    }
    return reverseNum;
}
```
上述代码中，我们使用模除运算 num % 10 来获取 num 的最后一位数字，并使用整除运算 num // 10 将其移除。然后将这个数字放置到 reverse_num 的最前面。由于是从个位数开始逐步反转，因此得到的结果是数字的反向版本。

值得注意的是，我们需要使用 // 而非 / 来进行整除运算，否则将返回浮点型结果而非整数。此外，初始时需要将 reverse_num 初始化为 0，否则在第一次循环时就不能正确执行加法操作。

回到题目这里来，整个实现如下
```java
public class Main {

    public static void main(String[] args) {
        int cnt = 0;
        for (int i = 2022; i <= 2022222022; i++) {
            if (isPalindromeAndMonotonous(i)) {
                cnt++;
            }
        }
        System.out.println(cnt);

    }

    public static boolean isPalindromeAndMonotonous(int num) {
        if (num %10 == 0) {
            return false;
        }
        int reverseNum = 0;
        while (num > reverseNum) {
            int b = num % 10;
            // b 是从个位数数起的
            // 如果上一个数大于当前的位数，不满足单调不增的原则
            if (reverseNum % 10 > b) {
                return false;
            }
            reverseNum = reverseNum * 10 + b;
            num /= 10;
        }

        // 偶数直接判断是否对称，奇数需要忽略中位数
        return reverseNum == num || reverseNum / 10 == num;
    }

}
```



## 练习题
[回文数](https://leetcode.cn/problems/palindrome-number/)
[回文链表](https://leetcode.cn/problems/palindrome-linked-list/)