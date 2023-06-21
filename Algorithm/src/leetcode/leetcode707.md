# 设计链表（leetcode707）

## 思路
### Java代码实现
```java
class MyLinkedList {

    private ListNode head;

    private int size;

    public MyLinkedList() {
        size = 0;
    }

    public int get(int index) {
        if (index < 0 || index > size - 1) {
            return -1;
        }
        if (index == 0) {
            return head.val;
        }
        ListNode cur = head;
        for (int i = 0; i < index; i++) {
            cur = cur.next;
        }
        return cur.val;
    }

    public void addAtIndex(int index, int val) {
        if (index < 0 || index > size) {
            return;
        }
        // 定义虚拟头节点
        ListNode dummyNode = new ListNode();
        ListNode node = new ListNode(val);
        dummyNode.next = head;
        ListNode pre = dummyNode;
        ListNode cur = dummyNode.next;
        for (int i = 0; i < index; i++) {
            pre = cur;
            cur = cur.next;
        }
        pre.next = node;
        node.next = cur;
        head = dummyNode.next;
        size++;
    }

    public void deleteAtIndex(int index) {
        if (index < 0 || index > size - 1) {
            return;
        }
        ListNode dummyNode = new ListNode();
        dummyNode.next = head;
        ListNode pre = dummyNode;
        ListNode cur = head;
        for (int i = 0; i < index; i++) {
            pre = cur;
            cur = cur.next;
        }
        pre.next = cur.next;
        head = dummyNode.next;
        size--;
    }

    public void addAtHead(int val) {
        addAtIndex(0, val);
    }

    public void addAtTail(int val) {
        addAtIndex(size, val);
    }
}

class ListNode {
    public int val;

    public ListNode next;

    public ListNode() {
    }

    public ListNode(int val) {
        this.val = val;
    }

    @Override
    public String toString() {
        return "ListNode{" + "val=" + val + ", next=" + next + '}';
    }
}
```
