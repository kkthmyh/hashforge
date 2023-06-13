# 有效的字母异位词（leetcode242）

## 思路
题干说明s和t是小写字母，所以可以看成索引为0-25，可以设置一个大小为26的数组，每个下标分别记录每个字母出现的个数
## Java代码实现
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        int[] arr = new int[26];
        // 按照相对字符a的位置的下标进行计数
        for (int i = 0; i < s.length(); i++) {
            arr[s.charAt(i) - 'a']++;
        }

        for (int i = 0; i < t.length(); i++) {
            // 如果t中存在s中包含的字符，那么相对位置的计数-1，否则不做处理，防止减法成负数
            if (arr[t.charAt(i) - 'a'] != 0) {
                arr[t.charAt(i) - 'a']--;
            }
        }
        return Arrays.stream(arr).sum() == 0;
    }
}
```