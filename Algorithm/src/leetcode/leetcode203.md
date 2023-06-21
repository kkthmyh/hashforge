# 移除链表元素（leetcode203）
## 思路
1、可以考虑虚拟头节点加双指针操作  
2、设置pre和cur指针，初始分别指向虚拟头节点和head节点  
3、当cur = val时候，pre指针指向cur，否则pre和cur都指向next  
## Java代码实现
```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        // 定义虚拟头节点
        ListNode dummyNode = new ListNode();
        dummyNode.next = head;

        ListNode pre = dummyNode;
        ListNode cur = dummyNode.next;
        while (pre.next != null) {
            if (cur.val == val) {
                pre.next = cur.next;
                pre = cur;
            }else {
                pre = cur;
            }
            cur = cur.next;
        }
        return dummyNode.next;
    }
}
```
