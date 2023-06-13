# 两个数组的交集（leetcode349）

## 思路
涉及到交集问题，首先想到Set集合。可以先定义2个Set1、Set2集合对两组元素进行去重复，再将第二组元素放入Set1，在第二组元素放入的时候需要判断下能否放入，不能放入的元素即为交集元素
## Java代码实现
```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        if (nums1.length == 0 || nums2.length == 0) {
            return new int[0];
        }
        // 定义2个Set进行第一遍数据去重
        Set<Integer> set1 = new HashSet<>();
        for (int num : nums1) {
            set1.add(num);
        }
        Set<Integer> set2 = new HashSet<>();
        for (int num : nums2) {
            set2.add(num);
        }
        List<Integer> list0 = new ArrayList<>(set2);
        List<Integer> list1 = new ArrayList<>();

        for (int num : list0) {
            // 无法放入Set证明是交集元素
            boolean flag = set1.add(num);
            if (!flag) {
                list1.add(num);
            }
        }
        int[] res = new int[list1.size()];

        for (int i = 0; i < list1.size(); i++) {
            res[i] = list1.get(i);
        }
        return res;
    }
}
```