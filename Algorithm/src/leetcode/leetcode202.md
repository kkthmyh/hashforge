# 快乐数（leetcode202）

## 思路
1、快乐数必然最后=1  
2、如果不是快乐数必然产生死循环，有点类似于环形链表，所以可以做为while循环的条件  
3、注意下一个n值的计算方法
## Java代码实现
```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> set = new HashSet<>();
        // 当set包含了n值证明产生环，所以退出循环
        while (n != 1 && !set.contains(n)) {
            set.add(n);
            n = getNextNum(n);
        }
        return n == 1;
    }

    public int getNextNum(int n) {
        int res = 0;
        while (n > 0) {
            int temp = n % 10;
            res += temp * temp;
            n = n / 10;
        }
        return res;
    }
}
```