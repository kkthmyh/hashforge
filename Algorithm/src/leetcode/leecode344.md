# 反转字符串（leetcode344）

## 思路
### 解法1:直接swap中心轴两边的元素    
观察得知，取中心轴对称，反转即交换中间字符两边的字符即可  
  


---
### 解法2:使用双指针swap  
1、定义left和right指针，使其分别指向第一个和最后一个字符  
2、开始swap两个指针指向的字符，swap之后，两个指针相互靠近，知道指针相遇即反转完毕  

## Java代码实现
```java
// 解法1
class Solution {
    public void reverseString(char[] s) {
        if (s.length <= 1) {
            return;
        }
        for (int i = 0; i < s.length; i++) {
            if (s.length / 2 > i) {
                char temp = s[i];
                s[i] = s[s.length - 1 - i];
                s[s.length - 1 - i] = temp;
            }
        }
    }
}
```
```java
// 解法2
class Solution {
    public void reverseString(char[] s) {
        if (s.length <= 1) {
            return;
        }
        int left = 0;
        int right = s.length - 1;
        // 反转条件
        while (left < right) {
            swap(s, left, right);
            left++;
            right--;
        }
    }

    private void swap(char[] chars, int left, int right) {
        char temp = chars[left];
        chars[left] = chars[right];
        chars[right] = temp;
    }
}
```