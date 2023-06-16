# 替换空格（剑指offer05）

## 思路
### 解法1:for循环判断空格进行处理，需要额外空间
直接for循环进行每个字符判断    

---
### 解法2:使用双指针 
1、先找出所有空格，进行原字符串扩容   
2、定义left和right指针，left初始指向扩容前字符串的最后一位字符，right指向扩容后字符串的最后一位字符  
3、移动left和right指针  

```java
// 解法1
class Solution {
    public String replaceSpace(String s) {
        List<Character> list = new ArrayList<>();
        if (s.length() == 0) {
            return s;
        }
        char[] arr = s.toCharArray();
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == ' ') {
                list.add('%');
                list.add('2');
                list.add('0');
            } else {
                list.add(arr[i]);
            }
        }
        char[] chars = new char[list.size()];
        for (int i = 0; i < chars.length; i++) {
            chars[i] = list.get(i);
        }
        return String.valueOf(chars);
    }
}
```
```java
class Solution {
    public String replaceSpace(String s) {
        if (s == null || s.length() == 0) {
            return s;
        }
        //扩充空间，空格数量2倍
        StringBuilder str = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == ' ') {
                str.append("  ");
            }
        }
        //若是没有空格直接返回
        if (str.length() == 0) {
            return s;
        }
        //有空格情况 定义两个指针
        int left = s.length() - 1;//左指针：指向原始字符串最后一个位置
        s += str.toString();
        int right = s.length() - 1;//右指针：指向扩展字符串的最后一个位置
        char[] chars = s.toCharArray();
        while (left >= 0) {
            if (chars[left] == ' ') {
                chars[right--] = '0';
                chars[right--] = '2';
                chars[right] = '%';
            } else {
                chars[right] = chars[left];
            }
            left--;
            right--;
        }
        return new String(chars);
    }
}
```