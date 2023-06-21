# 二叉树中序遍历（leetcode94）

## 思路
1、前序遍历，遍历顺序为左子树->根节点->右子树  
2、可以使用递归和迭代法遍历  

## Java代码实现
```java
// 递归法
class Solution {
    private List<Integer> list = new ArrayList<>();
    public List<Integer> inorderTraversal(TreeNode root) {
        if (root != null) {
            inorderTraversal(root.left);
            list.add(root.val);
            inorderTraversal(root.right);
        }
        return list;
    }
}
```

```java
// 迭代法，任何递归函数都可以用栈实现，所以迭代法使用栈遍历
class Solution {
     public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        TreeNode cur = root;
        Stack<TreeNode> stack = new Stack<>();
        while (cur != null || !stack.isEmpty()) {
            if (cur != null){
                stack.push(cur);
                cur = cur.left;
            }else{
                cur = stack.pop();
                res.add(cur.val);
                cur = cur.right;
            }
        }
        return res;
    }
}
```
