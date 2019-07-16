###  Question 387: First Unique Character in a String
---

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

**Examples:**

```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```



**Note:** You may assume the string contain only lowercase letters.

**Solution :**

```java
class Solution {
    public int firstUniqChar(String s) {
        if(s == null || s.length() == 0)
            return -1;
        if(s.length() == 1)
            return 0;
        for(int i = 0; i < s.length(); i++)
        {
            if(ifRepeat(s,i))
                return i;
        }
        return -1;   
    }
    public boolean ifRepeat(String s ,int n)
    {
        for(int i = 0 ; i < s.length(); i++)
        {
            if(i!=n  && s.charAt(n) == s.charAt(i))
                return false;
        }
        return true;
    }
}
```

**Approach 2: Hash map**

```java
class Solution {
    public int firstUniqChar(String s) {
        HashMap<Character,Integer> count = new HashMap<Character,Integer>();
        int n = s.length();
        for(int i = 0 ; i < n ;i++)
        {
            count.put(s.charAt(i),count.getOrDefault(s.charAt(i),0)+1);
        }
        
        for(int j = 0; j < n; j++)
        {
            if(count.get(s.charAt(j)) == 1)
                return j;
        }
        return -1;
    }
}
```

**Approach 3: use fixed array to increase speed.**

```java
class Solution {
    public int firstUniqChar(String s) {
        int[] count = new int[26];
        int n = s.length();
        // build char count bucket : <charIndex, count>
        for (int i = 0; i < n; i++) {            
            int index = s.charAt(i) - 'a';
            count[index]++;
        }
        
        // find the index
        for (int i = 0; i < n; i++) {
            int index = s.charAt(i) - 'a';
            if (count[index] == 1) {
                return i;
            }
                
        }
        return -1;
    }
}
```

