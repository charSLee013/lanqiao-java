##【问题描述】 
已知今天是星期六，请问 20 的 22 次方天后是星期几？ 注意用数字 1 到 7 表示星期一到星期日

## 解题思路
---

### 使用`Biginteger`
因为 20 的 22 次方是一个非常大的数，普通的整型变量无法存储，所以我们需要使用 Java 的 BigInteger 类来进行高精度运算。
BigInteger 类提供了一些方法来进行幂运算和取模运算，我们可以利用这些方法来求解

```java
import java.math.BigInteger; // 导入BigInteger类

public class Main {
    public static void main(String[] args) {
        BigInteger ans = BigInteger.valueOf(20).pow(22).mod(BigInteger.valueOf(\,7)); // 20的22次方对7取余
        ans = ans.add(BigInteger.valueOf(6)).mod(BigInteger.valueOf(\,7)); // 加上今天是星期六，再对7取余
        System.out.println(ans.equals(BigInteger.ZERO) ? 7 : ans); // 如果结果是0，输出7，否则输出结果
    }
}
```

得出

```
7
```

### 数学解题思路
我们先从20的1次方到4次方开始，看下有什么不同或者规律

```java
class Main{
    public static void main(String[] args) {
        display(6+20);
        display(6+20*20);
        display(6+20*20*20);
        display(6+20*20*20*20);
    }

    public static void display(int days){
        int day = days%7;
        System.out.println(day == 0 ? 7: day);
    }
}
```

得出结果
```
5
7
5
7
```

可以其中的规律，然后我们用数学公式来解释一下其中的规律
1. 首先来复习下$a^b\bmod n$取模公式

$$a^b \bmod n = ((a \bmod n)^b) \bmod n$$

其中，$\bmod$ 运算表示取模运算。这个公式的意思是，我们先对 $a$ 和 $n$ 分别进行取模运算，然后再将它们的幂次方相乘，最后再对 $n$ 取模，就得到了 $a^b\bmod n$ 的值。

2. 然后，我们把 a = 20 ， b = 22 ， n = 7 带入上式，得到：

把 a = 20 ， b = 22 ， n = 7 带入上式，得到：

$20^{22} \operatorname {mod}7 = (20 \operatorname {mod}\,7)^{22} \operatorname {mod}7$

$= (6)^{22} \operatorname {mod}7$

$20^{22}\;mod\;7=(20\;mod\;\,7)^{22}\;mod\;7=(6)^{22}\; mod\;7
$

接下来，我们把 b = 22 分解成 b = 2k + r ，其中 k 是整数， r 是余数（0 或者 1），得到：
$(6)^{2k + r} \operatorname {mod}\,7$

$= (6^2)^{k} × (6^r) \operatorname {mod}\,7$

$(6)^{2k+r} mod7=(6^2)^k × (6^r) mod \,7$

再接下来，我们利用模运算的另一个性质：
$$(a \times b) \mod n = ((a \mod n) \times (b \mod n)) \mod n$$
得到：

$(6^2)^k × (6^r) mod\,7=((6^2) mod\,\,7)^k × ((6^r) mod\,\,7) \;mod\,7$

最后，我们计算出 $(6^2) \operatorname {mod}7 和 (6^r) \operatorname {mod}7$ 的值，得到：
$(6^2) \operatorname {mod}\,7 = 36 \operatorname {mod}7 = 1$


```math
(6^r) \operatorname {mod}\,7 = \begin{cases}

1 & r = 0 \\

6 & r = 1 \\

\end{cases}
```

所以，当 r = 0 （即 b 是偶数）时，我们有：

```math
((6^2) \operatorname {mod}\,7)^k × ((6^r) \operatorname {mod}\,7) \operatorname {mod}7

\\= (1)^k × (1) \operatorname {mod}7

\\= 1 + 6 = 7
```

当 r = 1 （即 b 是奇数）时，我们有：

```math
((6^2) \operatorname {mod}\,7)^k × ((6^r) \operatorname {mod}\,7) \operatorname {mod}7

\\= (1)^k × (6) \operatorname {mod}7

\\= 6 + 6 = 12 \operatorname {mod}7

\\= 5
```

所以直接用数学的方式也能计算出来

## 练习题
---
[两数相加](https://leetcode.cn/problems/add-two-numbers-ii/)
[二进制求和](https://leetcode.cn/problems/add-binary/)
[蒸熟拆分](https://leetcode.cn/problems/integer-break/)