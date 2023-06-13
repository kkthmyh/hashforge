# 三数之和 (leetcode15)

## 思路
1、难点就是得想到用双指针，暴力解法时间复杂度过高，可能出现超时  
2、将数组进行升序排列，定义left和right指针  
3、通过nums[i]、nums[left]、nums[right]之和与0比较移动指针  
4、重点！！！要注意重复元素的去除，这里我开始很难理解num[i] == nums[i-1]时跳过当前循环，考虑此数组[-4,-1,-1,0,1,2]
当i=1时候，必定是枚举了右侧所有的可能,[-1,-1,2],[-1,-1,1],[-1,-1,0],所以当i=2时，三元组第一个元素nums[2]=nums[1],
必然存在一组值和上述枚举的可能性重合，所以需要跳过
## Java代码实现
```java
class Solution3 {

    public List<List<Integer>> threeSum(int[] nums) {

        // 定义返回结果集
        List<List<Integer>> res = new ArrayList<>();
        // 参数校验
        if (nums.length < 3) {
            return res;
        }
        // 将数组进行排序
        Arrays.sort(nums);

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > 1) {
                return res;
            }
            // 定义左右两指针
            int left = i + 1;
            int right = nums.length - 1;
            // 第一个位置重复则此次遍历结束，因为上一次遍历已经枚举出所有的组合，如果此次循环不结束会导致重复
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum > 0) {
                    // 右指针左移
                    right--;
                } else if (sum < 0) {
                    // 左指针右移
                    left++;
                } else {
                    // 需要进行收集元素
                    res.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    // 如果右指针的前一个数等于当前数，右指针持续左移
                    while (left < right && nums[right] == nums[right - 1]) {
                        right--;
                    }
                    // 如果左指针的后一个数等于当前数，左指针持续右移
                    while (left < right && nums[left] == nums[left + 1]) {
                        left++;
                    }
                    // 双指针同时移动
                    left++;
                    right--;
                }
            }
        }
        return res;
    }
}
```