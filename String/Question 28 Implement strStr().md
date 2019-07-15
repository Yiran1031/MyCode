### Question 28: Implement strStr()
---

Implement [strStr()](http://www.cplusplus.com/reference/cstring/strstr/).

Return the index of the first occurrence of needle in haystack, or **-1** if needle is not part of haystack.

**Example 1:**

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

**Example 2:**

```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

**Clarification:**

What should we return when `needle` is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's [strstr()](http://www.cplusplus.com/reference/cstring/strstr/) and Java's [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)).

**Solution**:

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.equals(""))
            return 0;
        int start = -1;
        int hay_length = haystack.length();
        int nee_length = needle.length();
        
        if(hay_length<nee_length)
            return -1;
        
        int h = 0;
        int n = 0;
        while(h < hay_length && n < nee_length)
        {
            if(haystack.charAt(h) == needle.charAt(n))
            {
                if(n == 0)
                {
                    start = h;
                }
                if(n == nee_length-1)
                    return start;
                h++;
                n++;
            }else
            {
                h = h - n+1;
                n = 0;
                start = -1;
            }
        }
        if(n!=nee_length)
            start = -1;
        return start;
    }
}
```

