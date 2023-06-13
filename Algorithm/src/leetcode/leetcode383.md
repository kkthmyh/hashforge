# 赎金信 (leetcode383)
## 思路
1、由题意知，magazines所包含的每个字母字符个数必须大于等于ransom，否则返回false  
2、可以考虑定义一个length为26的数组，索引0-25分别存储每个字符出现的个数  
3、遍历magazine将字符个数存入数组对应下标，遍历ransomNote将字符对应下标个数--  
4、最后的数组如果出现某一元素小于0，则返回false

## Java代码实现
```java
class Solution {

    public boolean canConstruct(String ransomNote, String magazine) {

        if (ransomNote.length() > magazine.length()) {
            return false;
        }

        int[] arr = new int[26];
        for (int i = 0; i < magazine.length(); i++) {
            arr[magazine.charAt(i) - 'a']++;
        }

        for (int i = 0; i < ransomNote.length(); i++) {
            arr[ransomNote.charAt(i) - 'a']--;
        }

        for (int num : arr) {
            if (num < 0) {
                return false;
            }
        }
        return true;
    }
}
```