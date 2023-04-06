##【问题描述】

给定一个只包含大写字母的字符串S，请你输出其中出现次数最多的字母。如果有多个字母均出现了最多次，按字母表顺序依次输出所有这些字母。

【输入格式】

一个只包含大写字母的字符串S.

【输出格式】

若干个大写字母，代表答案。

【样例输入】

BABBACAC

【样例输出】

AB

【评测用例规模与约定】

对于 100 %的评测用例， 1 ≤|S|≤106{^6}6


## 解题思路

### 暴力推算
直接 2n遍历数组
第一次是存储每个字母出现的次数
第二次是找出频率最高的那个
然后按顺序输出

```java
import java.util.ArrayList;

public  class Main {
    public static void main(String[] args) {
        System.out.println(MaxShow("BACDEQBA"));
        System.out.println(MaxShow("POIUYTREWQ"));

    }

    public static char[] MaxShow(String s){
        int len = s.length();
        char[] s_arr = s.toCharArray();
        int[] map = new int[26];


        // 遍历每个字母的数量
        for(int i = 0; i < len;i++){
            map[s_arr[i] - 'A'] ++;
        }

        ArrayList<Character> list = new ArrayList<>();
        int max =1;
        for(int i = 0; i < 26;i++){
            if(map[i] > max){
                list.clear();
                list.add((char)(i+'A'));
                max = map[i];
            } else if (map[i] == max){
                list.add((char)(i+'A'));
            }
        }

        char[] arr = new char[list.size()];
        for(int i = 0; i < arr.length;i++){
            arr[i] = list.get(i);
        }
        return arr;
    }
}
```


## 练习题
