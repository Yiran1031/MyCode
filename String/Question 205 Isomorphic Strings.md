###  Question 205: Isomorphic Strings
---

Given two strings **s** and **t**, determine if they are isomorphic.

Two strings are isomorphic if the characters in **s** can be replaced to get **t**.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

**Example 1:**

```
Input: s = "egg", t = "add"
Output: true
```

**Example 2:**

```
Input: s = "foo", t = "bar"
Output: false
```

**Example 3:**

```
Input: s = "paper", t = "title"
Output: true
```

**Note:**
You may assume both **s** and **t** have the same length.

**Solution: Using hash map**

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if(s==null || t == null)
            return false;
        if(s.length() != t.length())
            return false;
        // int[] m1 = new int[256];
        // int[] m2 = new int[256];
        HashMap<Character,Integer> hs = new HashMap<Character,Integer>();
        HashMap<Character,Integer> ht = new HashMap<Character,Integer>();
        for(int i = 0 ; i < s.length(); i++)
        {
            // if(m1[s.charAt(i)] != m2[t.charAt(i)]) return false;
            // m1[s.charAt(i)] = m2[t.charAt(i)] = i + 1;
            int m = hs.getOrDefault(s.charAt(i),-1); 
            int n = ht.getOrDefault(t.charAt(i),-1);
            if(m != n) return false;
            hs.put(s.charAt(i),i);
            ht.put(t.charAt(i),i);
        }
        return true;
    }
}
```