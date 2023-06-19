# 滑动窗口最大值（leetcode239）

## 思路
1、本题如果使用暴力解法，时间复杂度是O(n*m)，直接超时  
2、考虑单调队列，使用单调队列模拟滑动窗口  
3、当后入队元素大于前入队元素时，前入队元素需要出队  
4、滑动窗口每次移动时，队首元素进行出队列

### Java代码实现
```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        // 窗口大小为1，直接返回原数组
        if (k == 1) {
            return nums;
        }
        MyQueue deque = new MyQueue();
        int[] res = new int[nums.length - k + 1];
        int num = 0;
        // 前k个元素直接加入队列
        for (int i = 0; i < k; i++) {
            deque.push(nums[i]);
        }
        res[num++] = deque.peek();
        for (int i = k; i < nums.length; i++) {
            // 当前元素等于队首元素进行出队
            deque.poll(nums[i - k]);
            deque.push(nums[i]);
            res[num++] = deque.peek();
        }
        return res;
    }

    class MyQueue {
        Deque<Integer> deque;

        public MyQueue() {
            deque = new LinkedList<>();
        }

        void poll(int val){
            if (!deque.isEmpty() && val == deque.peek()) {
                deque.poll();
            }
        }

        void push(int val) {
            while (!deque.isEmpty() && val > deque.getLast()) {
                deque.removeLast();
            }
            deque.add(val);
        }

        int peek() {
            return deque.peek();
        }
    }
}
```
