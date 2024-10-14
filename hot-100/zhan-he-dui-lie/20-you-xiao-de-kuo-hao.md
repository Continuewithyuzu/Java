# 20、有效的括号

一开始写的代码：考虑的情况不够全面

```java
class Solution {
    public boolean isValid(String s) {
        //Stack<String> stack = new Stack();
        int len = s.length();
        for (int i = 0, j = len-1; i < len/2 && j >= len/2; i++,j--) {
            char c1 = s.charAt(i);
            char c2 = s.charAt(j);
            if (c1=='(' && c2 ==')' ||c1 == '{' && c2 =='}' || c1 == '[' && c2 == ']') {
                continue;
            }
            else{
                return false;
            }
        }
        return true;
    }
}
```

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>



## 题解：

我们遍历给定的字符串 s。当我们遇到一个左括号时，我们会期望在后续的遍历中，有一个相同类型的右括号将其闭合。由于后遇到的左括号要先闭合，因此我们可以将这个左括号放入栈顶。

当我们遇到一个右括号时，我们需要将一个相同类型的左括号闭合。此时，我们可以取出栈顶的左括号并判断它们是否是相同类型的括号。如果不是相同的类型，或者栈中并没有左括号，那么字符串 s 无效，返回 False。为了快速判断括号的类型，我们可以使用哈希表存储每一种括号。哈希表的键为右括号，值为相同类型的左括号。

在遍历结束后，如果栈中没有左括号，说明我们将字符串 s 中的所有左括号闭合，返回 True，否则返回 False。

注意到有效字符串的长度一定为偶数，因此如果字符串的长度为奇数，我们可以直接返回 False，省去后续的遍历判断过程。

建立hash表是为了构建左右括号对应关系：$$key$$ 左括号，$$value$$ 右括号；这样查询 $$2$$ 个括号是否对应只需 $$O(1)$$ 时间复杂度；

```java
class Solution {
    public boolean isValid(String s) {
        int n = s.length();
        if (n % 2 == 1) {
            return false;
        }

        Map<Character, Character> pairs = new HashMap<Character, Character>() {{
            put(')', '(');
            put(']', '[');
            put('}', '{');
        }};
        Deque<Character> stack = new LinkedList<Character>();
        for (int i = 0; i < n; i++) {
            char ch = s.charAt(i);
            if (pairs.containsKey(ch)) {
                if (stack.isEmpty() || stack.peek() != pairs.get(ch)) {
                    return false;
                }
                stack.pop();
            } else {
                stack.push(ch);
            }
        }
        return stack.isEmpty();
    }
}
```

执行用时更少的代码：1ms

```java
class Solution {
    public boolean isValid(String s) {
        LinkedList<Character> stack = new LinkedList<>();
        for(char c:s.toCharArray()){
            if(c=='('||c=='{'||c=='[')stack.push(c);
            else {
                if(stack.isEmpty())return false;
                char pop = stack.pop();
                if(c==']'&&pop=='['||c=='}'&&pop=='{'||c==')'&&pop=='(');
                else return false;
            }
        }
        if(stack.isEmpty())return true;
        return false;
    }
}
```

原理就是，如果符号位左边的符号，push进栈，如果是右边的就取出栈顶元素，看是否对应，否则返回false。
