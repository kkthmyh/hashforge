# 四数之和 (leetcode18)

## 思路
1、此题是leetcode15升级版本，需要leetcode15前置知识  
2、注意剪枝，这里剪枝不能仅判断nums[i]>target,因为nums[i]可能为负数，考虑数组[-4,-2,0,3],target = -3,所以break的条件应为
nums[i]>target&&nums[i]>0
## Java代码实现
```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {

        List<List<Integer>> res = new ArrayList<>();

        if (nums.length < 4) {
            return res;
        }

        Arrays.sort(nums);

        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            if (nums[i] > target && nums[i] > 0) {
                break;
            }
            for (int j = i + 1; j < nums.length; j++) {
                if (j > i + 1 && nums[j - 1] == nums[j]) {
                    continue;
                }
                int left = j + 1;
                int right = nums.length - 1;

                while (left < right) {
                    int sum = nums[i] + nums[j] + nums[left] + nums[right];
                    if (sum > target) {
                        right--;
                    } else if (sum < target) {
                        left++;
                    } else {
                        res.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));
                        while (left < right && nums[right] == nums[right - 1]) {
                            right--;
                        }
                        while (left < right && nums[left] == nums[left + 1]) {
                            left++;
                        }
                        right--;
                        left++;
                    }
                }
            }
        }
        return res;
    }
}
```