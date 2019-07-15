###  Question 14 : Longest Common Prefix！
---

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

```
Input: ["flower","flow","flight"]
Output: "fl"
```

**Example 2:**

```
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

**Note:**

All given inputs are in lowercase letters `a-z`.

### Solution
---

#### Approach 1: Horizontal scanning

**Intuition**

For a start we will describe a simple way of finding the longest prefix shared by a set of strings LCP(S_1 \ldots S_n)*L**C**P*(*S*1…*S**n*). We will use the observation that :

LCP(S_1 \ldots S_n) = LCP(LCP(LCP(S_1, S_2),S_3),\ldots S_n)*L**C**P*(*S*1…*S**n*)=*L**C**P*(*L**C**P*(*L**C**P*(*S*1,*S*2),*S*3),…*S**n*)

**Algorithm**

To employ this idea, the algorithm iterates through the strings [S_1 \ldots S_n][*S*1…*S**n*], finding at each iteration i*i* the longest common prefix of strings LCP(S_1 \ldots S_i)*L**C**P*(*S*1…*S**i*) When LCP(S_1 \ldots S_i)*L**C**P*(*S*1…*S**i*) is an empty string, the algorithm ends. Otherwise after n*n* iterations, the algorithm returns LCP(S_1 \ldots S_n)*L**C**P*(*S*1…*S**n*).

![Finding the longest common prefix](https://leetcode.com/media/original_images/14_basic.png)

*Figure 1. Finding the longest common prefix (Horizontal scanning)*

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0)
            return "";
        String prefix = strs[0];
        for(int i = 0; i < strs.length;i++)
        {
            while(strs[i].indexOf(prefix)!=0)
            {
                prefix = prefix.substring(0,prefix.length() - 1 );
            }
            if(prefix.isEmpty()) return "";
        }
        
        return prefix;
    }
}
```

---

#### Approach 2: Vertical scanning

**Algorithm**

Imagine a very short string is at the end of the array. The above approach will still do *S* comparisons. One way to optimize this case is to do vertical scanning. We compare characters from top to bottom on the same column (same character index of the strings) before moving on to the next column.

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0)
            return "";
        for(int i = 0; i < strs[0].length();i++)
        {
            char c = strs[0].charAt(i);
            for(int j = 1; j < strs.length;j++)
            {
                if(i == strs[j].length()||strs[j].charAt(i) != c)
                    return strs[0].substring(0,i);
            }
        }
        
        return strs[0];
    }
}
```

**Complexity Analysis**

- Time complexity : O(S)*O*(*S*) , where S is the sum of all characters in all strings. In the worst case there will be n*n* equal strings with length m*m* and the algorithm performs S = m \cdot n*S*=*m*⋅*n* character comparisons. Even though the worst case is still the same as [Approach 1](https://leetcode.com/problems/longest-common-prefix/solution/#approach-1-horizontal-scanning), in the best case there are at most n \cdot minLen*n*⋅*m**i**n**L**e**n* comparisons where minLen*m**i**n**L**e**n* is the length of the shortest string in the array.
- Space complexity : O(1)*O*(1). We only used constant extra space. 

---

#### Approach 3: Divide and conquer

**Intuition**

The idea of the algorithm comes from the associative property of LCP operation. We notice that : LCP(S_1 \ldots S_n) = LCP(LCP(S_1 \ldots S_k), LCP (S_{k+1} \ldots S_n))*L**C**P*(*S*1…*S**n*)=*L**C**P*(*L**C**P*(*S*1…*S**k*),*L**C**P*(*S**k*+1…*S**n*)) , where LCP(S_1 \ldots S_n)*L**C**P*(*S*1…*S**n*) is the longest common prefix in set of strings [S_1 \ldots S_n][*S*1…*S**n*] , 1 < k < n1<*k*<*n*

**Algorithm**

To apply the observation above, we use divide and conquer technique, where we split the LCP(S_i \ldots S_j)*L**C**P*(*S**i*…*S**j*) problem into two subproblems LCP(S_i \ldots S_{mid})*L**C**P*(*S**i*…*S**m**i**d*) and LCP(S_{mid+1} \ldots S_j)*L**C**P*(*S**m**i**d*+1…*S**j*), where `mid` is \frac{i + j}{2}2*i*+*j*. We use their solutions `lcpLeft` and `lcpRight`to construct the solution of the main problem LCP(S_i \ldots S_j)*L**C**P*(*S**i*…*S**j*). To accomplish this we compare one by one the characters of `lcpLeft` and `lcpRight` till there is no character match. The found common prefix of `lcpLeft` and `lcpRight` is the solution of the LCP(S_i \ldots S_j)*L**C**P*(*S**i*…*S**j*).

![Finding the longest common prefix](https://leetcode.com/media/original_images/14_lcp_diviso_et_lmpera.png)

*Figure 2. Finding the longest common prefix of strings using divide and conquer technique*



```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs == null || strs.length == 0) return "";
        return longestCommonPrefix(strs,0,strs.length-1);
    }
    public String longestCommonPrefix(String[] strs, int l,int r)
    {
        if(l==r)
        {
              return strs[l];   
        }else
        {
            int mid = (l+r)/2;
            String left = longestCommonPrefix(strs,l,mid);
            String right = longestCommonPrefix(strs,mid+1,r);
            return longestCommonPrefix(left,right);
        }
    }
    public String longestCommonPrefix(String left, String right)
    {
        int length = Math.min(left.length(),right.length());
        for(int i = 0 ; i < length; i++ )
        {
            if(left.charAt(i) != right.charAt(i))
                return left.substring(0,i);
        }
        return left.substring(0,length);
    }
}
```

**Complexity Analysis**

In the worst case we have n*n* equal strings with length m*m*

- Time complexity : O(S)*O*(*S*), where S*S* is the number of all characters in the array, S = m \cdot n*S*=*m*⋅*n* Time complexity is 2 \cdot T\left ( \frac{n}{2} \right ) + O(m)2⋅*T*(2*n*)+*O*(*m*). Therefore time complexity is O(S)*O*(*S*). In the best case this algorithm performs O(minLen \cdot n)*O*(*m**i**n**L**e**n*⋅*n*) comparisons, where minLen*m**i**n**L**e**n* is the shortest string of the array

- Space complexity : O(m \cdot \log n)*O*(*m*⋅log*n*)

  There is a memory overhead since we store recursive calls in the execution stack. There are \log nlog*n* recursive calls, each store need m*m* space to store the result, so space complexity is O(m \cdot \log n)*O*(*m*⋅log*n*)
  
---

#### Approach 4: Binary search

The idea is to apply binary search method to find the string with maximum value `L`, which is common prefix of all of the strings. The algorithm searches space is the interval (0 \ldots minLen)(0…*m**i**n**L**e**n*), where `minLen` is minimum string length and the maximum possible common prefix. Each time search space is divided in two equal parts, one of them is discarded, because it is sure that it doesn't contain the solution. There are two possible cases:

- `S[1...mid]` is not a common string. This means that for each `j > i S[1..j]` is not a common string and we discard the second half of the search space.
- `S[1...mid]` is common string. This means that for for each `i < j S[1..i]` is a common string and we discard the first half of the search space, because we try to find longer common prefix.

![Finding the longest common prefix](https://leetcode.com/media/original_images/14_lcp_binary_search.png)

*Figure 3. Finding the longest common prefix of strings using binary search technique*


```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs == null || strs.length == 0)
            return "";
        int minLen = Integer.MAX_VALUE;
        for(String str: strs)
            minLen = Math.min(minLen,str.length());
        int low = 1;
        int high = minLen;
        while(low <= high)
        {
            int middle = (low+high)/2;
            if(longestCommonPrefix(strs,middle))
            {
                low = middle + 1;
            }else
            {
                high = middle - 1;
            }
        }
        return strs[0].substring(0,(low+high)/2);
    }
    
    public boolean longestCommonPrefix(String[] strs, int len)
    {
        String substr = strs[0].substring(0,len);
        for(int i = 0; i < strs.length; i++)
        {
            if(!strs[i].startsWith(substr))
                return false;
        }
        return true;
    }
}
```