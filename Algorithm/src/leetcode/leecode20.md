# 有效的括号（leetcode20）

## 思路
1、利用栈的后进先出和记录前一个元素的特性，考虑使用栈来解题  
2、定义一个栈，遍历目标字符串遇见左括号时，向栈中push一个与其匹配的右括号  
3、遍历目标字符串遇见右括号时，进行peek元素，校验peek的元素与当前元素是否相等，如果相等栈顶元素出栈  
4、判断栈是否为empty，如是empty说明左右括号完全匹配，反之则不匹配  

## Java代码实现
```java
class Solution {
    public boolean isValid(String s) {
        // 奇数不符合
        if (s.length() == 0 || s.length() % 2 != 0) {
            return false;
        }
        Stack<Character> stack = new Stack<>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            // 如果是左括号，则向栈中压入对应右括号
            switch (c) {
                case '(':
                    stack.push(')');
                    break;
                case '{':
                    stack.push('}');
                    break;
                case '[': {
                    stack.push(']');
                    break;
                }
            }
            // 右括号情况
            if (c == ')' || c == '}' || c == ']') {
                // 判断栈是否为空,如果为空证明第一个字符是右括号，直接返回false
                if (!stack.isEmpty()) {
                    char peek = stack.peek();
                    // 如果当前字符和栈顶元素相同进行出栈,反之直接返回false
                    if (c == peek) {
                        stack.pop();
                    } else {
                        return false;
                    }
                } else {
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }
}
```