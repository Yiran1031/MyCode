###  Question 383: Ransom Note
---

Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

Each letter in the magazine string can only be used once in your ransom note.

**Note:**
You may assume that both strings contain only lowercase letters.

```java
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

**Solution: **

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        if(magazine == null || ransomNote.length() > magazine.length())
            return false;
        if(ransomNote.length() == 0)
            return true;
        int[] count_r = new int[26];
        int[] count_m = new int[26];
        for(int i = 0 ; i < ransomNote.length(); i++)
        {
            int index = ransomNote.charAt(i) - 'a';
            count_r[index]++;
        }
        
        for(int i = 0 ; i < magazine.length(); i++)
        {
            int index = magazine.charAt(i) - 'a';
            count_m[index]++;
        }
        
        for(int i = 0 ; i < 26; i++)
        {
            if(count_r[i] > count_m[i])
                return false;
        }
        return true;
    }
}
```