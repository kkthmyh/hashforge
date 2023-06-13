# 四数相加II (leetcode454)

## 思路
1、定义一个Hash表，key存nums1和nums2两两相加的和，value存同样的和出现的次数  
2、取0减num3，nums4两两之和为target，判断其是否存在于步骤1定义的map中  
3、若存在则++  
4、统计最后结果返回  

## Java代码实现
```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        // 定义一个map，其中key是两两相加的值，value是值出现的次数
        Map<Integer, Integer> map = new HashMap<>();
        
        for (int num1 : nums1) {
            for (int num2 : nums2) {
                int key = num1 + num2;
                if (!map.containsKey(key)) {
                    map.put(key, 1);
                } else {
                    map.put(key, map.get(key) + 1);
                }
            }
        }

        int count = 0;
        for (int num3 : nums3) {
            for (int num4 : nums4) {
                // 表示期望在map中获得target值，一旦获取到，则代表改路径是一个满足规则的解
                int target = -(num3 + num4);
                if (map.containsKey(target)) {
                    count += map.get(target);
                }
            }
        }
        return count;
    }
}
```