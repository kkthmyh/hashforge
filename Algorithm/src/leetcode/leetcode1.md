# 两数之和 (leetcode1)

## 思路
Hash表解决，没啥说的
## Java代码实现
```java
class Solution {
    // hash表
    public int[] twoSum(int[] nums, int target) {
       Map<Integer,Integer> map = new HashMap<>();
       int [] res = new int[2];
       for (int i = 0;i < nums.length;i++) {
           if (map.containsKey(target - nums[i])) {
               res[0] = i;
               res[1] = map.get(target - nums[i]);
           }
           map.put(nums[i],i);
       }
       return res;
    }
}
```