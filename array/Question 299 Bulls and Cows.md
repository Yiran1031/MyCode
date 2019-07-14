### Question 299: Bulls and Cows
---
You are playing the following [Bulls and Cows](https://en.wikipedia.org/wiki/Bulls_and_Cows) game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.

Write a function to return a hint according to the secret number and friend's guess, use `A`to indicate the bulls and `B` to indicate the cows. 

Please note that both secret number and friend's guess may contain duplicate digits.

Example:
```
Input: secret = "1807", guess = "7810"

Output: "1A3B"

Explanation: 1 bull and 3 cows. The bull is 8, the cows are 0, 1 and 7.
```
```
Input: secret = "1123", guess = "0111"

Output: "1A1B"

Explanation: The 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow.
```

**Note:** You may assume that the secret number and your friend's guess only contain digits, and their lengths are always equal.



**Solution : 2 Bucket**

```java
class Solution {
    public String getHint(String secret, String guess) {
        int cows  = 0;
        int bulls = 0;
        int[] sec = new int[10];
        int[] gue = new int[10];
        for(int i = 0; i < secret.length();i++)
        {
            if(secret.charAt(i) != guess.charAt(i))
            {
                sec[secret.charAt(i)-'0']++;
                gue[guess.charAt(i)-'0']++;
            }else
            {
                bulls++;
            }
        }
        
        for(int j = 0; j<10;j++)
        {
            cows = cows + Math.min(sec[j],gue[j]);
        }
        
        return bulls+"A"+cows+"B";
    }
}
```

