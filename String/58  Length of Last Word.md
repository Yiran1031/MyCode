###  58 : Length of Last Word
---

Given a string *s* consists of upper/lower-case alphabets and empty space characters `' '`, return the length of last word in the string.

If the last word does not exist, return 0.

**Note:** A word is defined as a character sequence consists of non-space characters only.

**Example:**

```java
Input: "Hello World"
Output: 5
```

**Solution :**

```java
class Solution {
    public int lengthOfLastWord(String s) {
        int len = s.length();
        int word = 0;
        int index = len-1;
        if(len == 0)
            return word;
        //remove the space at the end
        for(int i = len-1; i>= 0; i--)
        {
            if(s.charAt(i)!=' ')
                break;
            index--;
        }
        for(int i = index; i >=0 ; i--)
        {
            if(s.charAt(i) == ' ' )
            {
               return word;
            }else
            {
                word++;
            }
        }
        return word;
    }
}
```

