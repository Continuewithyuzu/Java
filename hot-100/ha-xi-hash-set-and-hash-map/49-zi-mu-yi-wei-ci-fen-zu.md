# 49、字母易位词分组

能反应过来用Hash 到了字符串拆分那一步不会拆分字符串

value：字母

key：不知道

~~看完代码随想录，key可以是0\~25，a\~z一一映射~~

* ~~需要把字符映射到数组也就是哈希表的索引下标上，**因为字符a到字符z的ASCII是26个连续的数值，所以字符a映射为下标0，相应的字符z映射为下标25。**~~

## **解题思路：**

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Hash表中的示意图：

```java
Hash{
    "aet": ["eat", "tea", "ate"],
    "ant": ["tan", "nat"],
    "abt": ["bat"]
}
```

按照思路写的代码：

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if(strs == null || strs.length == 0) return new ArrayList<List<String>>();
        HashMap<String, List<String>> map = new HashMap<String, List<String>>();
        for(String s : strs){
            char[] chars = s.toCharArray();//将字符串转为数组
            Arrays.sort(chars);//对数组字母进行排序
            String sortedstr = new String(chars);//排序后转为字符串
            if(!map.containsKey(sortedstr)){
                map.put(sortedstr,new ArrayList<>());
            }
            map.get(sortedstr).add(s);
        }
        //return new ArrayList<List<String>>(map.values());
        return new ArrayList<>(map.values());
        //两种返回都可以，后者运行时间少1ms
    }

```
