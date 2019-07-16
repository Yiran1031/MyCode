### Question 151: Reverse Words in a String !
---

Given an input string, reverse the string word by word.

 

**Example 1:**

```
Input: "the sky is blue"
Output: "blue is sky the"
```

**Example 2:**

```
Input: "  hello world!  "
Output: "world! hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

**Example 3:**

```
Input: "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

 

**Note:**

- A word is defined as a sequence of non-space characters.
- Input string may contain leading or trailing spaces. However, your reversed string should not contain leading or trailing spaces.
- You need to reduce multiple spaces between two words to a single space in the reversed string.



**Solution :**

There are 3 step in this solution

1. reverse the string.
2. reverse each word in the string.
3. remove extra space.

```java
class Solution {
    public String reverseWords(String s) {
        if(s == null)
            return null;
        char[] c = s.toCharArray();
        int n  = c.length;
        //step 1
        reverseString(c,0,n-1);
        //step 2
        reverseWord(c);
        //step 3
        return   cleanSpace(c);
    }
    public void reverseString(char[] c, int front, int end)
    {
        while(front < end)
        {
            char temp = c[end];
            c[end--] = c[front];
            c[front++] = temp;
        }
    }
    
    public void reverseWord(char[] c)
    {
        int s = 0, i = 0;
        while(s < c.length)
        {
            while(s < c.length && c[s] == ' ')s++;
            i = s;
            while(i < c.length && c[i] != ' ')i++;
            reverseString(c,s,i-1);
            s = i;
        }
    }
    public String cleanSpace(char[] c)
    {
        int i = 0, j = 0;
        while(j < c.length)
        {
            while(j < c.length && c[j] == ' ') j++;
            while(j < c.length && c[j] != ' ') c[i++] = c[j++];
            while(j < c.length && c[j] == ' ') j++;
            if(j < c.length) c[i++] = ' ';
        }
        return new String(c).substring(0,i);
    }
}
```

