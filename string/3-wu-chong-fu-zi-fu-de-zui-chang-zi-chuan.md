# 3、无重复字符的最长字串

## 题目描述

> 给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长 子串** 的长度。
>
> &#x20;
>
> **示例 1:**
>
> <pre><code><strong>输入: s = "abcabcbb"
> </strong><strong>输出: 3 
> </strong><strong>解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
> </strong></code></pre>
>
> **示例 2:**
>
> <pre><code><strong>输入: s = "bbbbb"
> </strong><strong>输出: 1
> </strong><strong>解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
> </strong></code></pre>
>
> **示例 3:**
>
> <pre><code><strong>输入: s = "pwwkew"
> </strong><strong>输出: 3
> </strong><strong>解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
> </strong><strong>     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
> </strong></code></pre>
>
> &#x20;
>
> **提示：**
>
> * `0 <= s.length <= 5 * 104`
> * `s` 由英文字母、数字、符号和空格组成

## 题解：

### 核心思路

* 使用两个指针左指针 `i`**和**右指针 `rk`来表示一个窗口，窗口内的子串是当前没有重复字符的最长子串。
* 使用一个哈希集合 `occ`来记录窗口内已经出现过的字符，确保窗口内的字符都是唯一的。

### 具体步骤

1. **初始化：**
   * 使用一个哈希集合 `occ` 来存储当前窗口中的字符，保证每个字符在窗口内不重复。
   * `n` 为字符串的长度。
   * `rk` 为右指针，初始值设置为 `-1`，表示右指针还没有开始移动。
   * `ans` 用于记录目前为止找到的最长子串的长度。
2. **遍历字符串：**
   * 通过外层循环遍历字符串 `s`，使用 `i` 来作为左指针的索引。
3. **更新左指针：**
   * 在每次移动左指针 `i` 时，如果 `i != 0`，则将 `i-1` 位置的字符从哈希集合 `occ` 中移除。因为当左指针向右移动时，窗口左边界的字符不再属于窗口。
4. **移动右指针：**
   * 右指针 `rk` 初始值是 `-1`，通过 `while` 循环不断移动右指针，直到窗口中的字符不再重复。
   * 在每次右指针移动时，将新的字符添加到哈希集合 `occ` 中。
   * 如果字符已经存在于集合中，说明窗口内的字符重复了，停止向右扩展窗口。
5. **计算当前窗口的长度：**
   * 每次右指针更新后，窗口内的子串就是从左指针 `i` 到右指针 `rk` 的子串，长度为 `rk - i + 1`。
   * 更新 `ans` 为当前窗口的最大长度：`ans = Math.max(ans, rk - i + 1)`。
6. **返回结果：**
   * 最后返回 `ans`，即字符串中没有重复字符的最长子串的长度。

### 时间复杂度

* 每个字符最多会被左指针和右指针访问一次，因此时间复杂度是 O(n)，其中 `n` 是字符串的长度。

```java
import java.util.HashSet;
import java.util.Set;

public class LongestSubstring {
    public int lengthOfLongestSubstring(String s) {
        // 哈希集合，记录每个字符是否出现过
        Set<Character> occ = new HashSet<Character>();
        int n = s.length();
        // 右指针，初始值为 -1，相当于我们在字符串的左边界的左侧，还没有开始移动
        int rk = -1, ans = 0;
        for (int i = 0; i < n; i++) {
            if (i != 0) {
                // 左指针向右移动一格，移除一个字符
                occ.remove(s.charAt(i - 1));
            }
            while (rk + 1 < n && !occ.contains(s.charAt(rk + 1))) {
                // 不断地移动右指针
                occ.add(s.charAt(rk + 1));
                rk++;
            }
            // 第 i 到 rk 个字符是一个极长的无重复字符子串
            ans = Math.max(ans, rk - i + 1);
        }
        return ans;
    }
}
```
