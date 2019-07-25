### Question 344: Reverse String
---

Write a function that reverses a string. The input string is given as an array of characters `char[]`.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

You may assume all the characters consist of [printable ascii characters](https://en.wikipedia.org/wiki/ASCII#Printable_characters).

 

**Example 1:**

```
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

**Example 2:**

```
Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

**Solution 1:**

```java
class Solution {
    public void reverseString(char[] s) {
        int front = 0;
        int end = s.length-1;
        while(front < end)
        {
            char temp = s[end];
            s[end] = s[front];
            s[front] = temp;
            end--;
            front++;
        }
    }
}
```

**Solution 2 : Recursion**

```java
class Solution {
    public void reverseString(char[] s) {
        if(s.length <= 1)
            return;
        reverse(s,0,s.length-1);
    }
    
    public void reverse(char[] c, int i, int j)
    {
        if(i > j)
            return;
        char temp = c[j];
        c[j] = c[i];
        c[i] = temp;
        reverse(c,i+1,j-1);
    }
}
```

```java
public class validParentheses
{
	public List<String> validParentheses(int k)
  {
    // the final String contains 2k characters.
    char[] cur = new char[k * 2];
    helper(cur,k,k,0,result);
    return result;
  }
  
  //left: how many '(' we still have;
  //right: how many ')' we still have;
  //index: the current position in cur we want to fill in
  // with either '(' or ')';
  private void helper(char[] cur,int left, int right, in index, List<String> result)
  {
    //terminate condition
    //when we do not have any parentheses left.
    if(left == 0 && right == 0)
    {
      result.add(new String(cur));
      return;
    }
    
    //when we can add a '(' ? whenever there is some '(' we can still use.
    if(left > 0)
    {
      cur[index] = '(';
      helper(curm left - 1, right, index + 1, result);
    }
    id(right > left)
    {
      cur[index] = ')';
      helper(cur,left,right - 1, index + 1, result);
    }
  } 
}
```

