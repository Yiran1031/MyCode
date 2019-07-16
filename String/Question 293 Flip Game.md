### Question 293: Flip Game
---

You are playing the following Flip Game with your friend: Given a string that contains only these two characters: `+` and `-`, you and your friend take turns to flip two **consecutive**`"++"` into `"--"`. The game ends when a person can no longer make a move and therefore the other person will be the winner.

Write a function to compute all possible states of the string after one valid move.

**Example:**

```
Input: s = "++++"
Output: 
[
  "--++",
  "+--+",
  "++--"
]
```

**Note:** If there is no valid move, return an empty list `[]`.

**Solution:**

```java
class Solution {
    public List<String> generatePossibleNextMoves(String s) {
        int n = s.length();
        int i = 0;
        List<String> ls = new ArrayList<String>();
        for(int j = 0; j < s.length()-1;j++)
        {
            if(s.charAt(j) == '+'  && s.charAt(j+1) == '+')
            {
                char[] c = s.toCharArray();
                c[j] = '-';
                c[j+1] = '-';
                ls.add(new String(c));
            }
        }
        return ls;
    }
}
```

