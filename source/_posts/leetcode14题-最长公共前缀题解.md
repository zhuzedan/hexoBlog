### leetcode14题-最长公共前缀题解



> 知识点盲区补充

Java中的startsWith()方法

startsWith(String str)就是检查形参参数是否与你要检查的字符串开头相同

startsWith(Sring str,int Index)则是从你要比较的原字符串的指定下标开始和形参作比较

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        String selectOne = "";
        if (strs.length == 0) {
            return "";
        }
        String s = strs[0];
        for (String string:strs){
            while (!string.startsWith(s)) {
                if (s.length() == 0) {
                    return "";
                }
                s = s.substring(0,s.length()-1);
            }
        }
        return s;
    }
}
```



字典序概念

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        //按字符串长度排序(字典序)
        Arrays.sort(strs);

        //比较第一个各最后一个
        String first = strs[0];
        String last = strs[strs.length - 1];

        for (int i = 0; i < first.length(); i++) {
            if (first.charAt(i) != last.charAt(i)) {
                return first.substring(0, i);
            }
        }
        return first;
    }
}
```