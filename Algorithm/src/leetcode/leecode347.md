# 前k个高频率元素（leetcode347）

## 思路
1、类似top K问题，首先考虑小顶堆，即优先队列  
2、定义map，key为元素，value为元素的出现的频率  

## Java代码实现
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {

        Map<Integer, Integer> map = new HashMap<>();
        // 统计出现次数
        for (int i = 0; i < nums.length; i++) {
            map.put(nums[i], map.getOrDefault(nums[i], 0) + 1);
        }
        // 定义小顶堆，存储数组，数组index0存储元素，index1存储其出现的次数
        PriorityQueue<int[]> queue = new PriorityQueue<>(Comparator.comparingInt(o -> o[1]));
        
        map.forEach((key, value) -> {
            int[] arr = new int[2];
            arr[0] = key;
            arr[1] = value;
            if (queue.size() < k) {
                queue.add(arr);
            } else {
                int[] peek = queue.peek();
                if (peek[1] < value) {
                    queue.poll();
                    queue.add(arr);
                }
            }
        });
        
        int[] res = new int[k];
        
        for (int i = res.length - 1; i >= 0; i--) {
            res[i] = queue.poll()[0];
        }
        return res;
    }
}
```
