###  Question 277: Find the Celebrity
---
Suppose you are at a party with ``n`` people (labeled from ``0`` to`` n - 1``) and among them, there may exist one celebrity. The definition of a celebrity is that all the other n - 1 people know him/her but he/she does not know any of them.

Now you want to find out who the celebrity is or verify that there is not one. The only thing you are allowed to do is to ask questions like: "Hi, A. Do you know B?" to get information of whether A knows B. You need to find out the celebrity (or verify there is not one) by asking as few questions as possible (in the asymptotic sense).

You are given a helper function ``bool knows(a, b)`` which tells you whether A knows B. Implement a function ``int findCelebrity(n)``. There will be exactly one celebrity if he/she is in the party. Return the celebrity's label if there is a celebrity in the party. If there is no celebrity, return ``-1``.

**Example:**

![img](https://assets.leetcode.com/uploads/2019/02/02/277_example_1_bold.PNG)

```
Input: graph = [
  [1,1,0],
  [0,1,0],
  [1,1,1]
]
Output: 1
Explanation: There are three persons labeled with 0, 1 and 2. graph[i][j] = 1 means person i knows person j, otherwise graph[i][j] = 0 means person i does not know person j. The celebrity is the person labeled as 1 because both 0 and 2 know him but 1 does not know anybody.
```

![img](https://assets.leetcode.com/uploads/2019/02/02/277_example_2.PNG)

```
Input: graph = [
  [1,0,1],
  [1,1,0],
  [0,1,1]
]
Output: -1
Explanation: There is no celebrity.
```

**Note:**

1. The directed graph is represented as an adjacency matrix, which is an `n x n` matrix where `a[i][j] = 1` means person `i` knows person `j` while `a[i][j] = 0` means the contrary.
2. Remember that you won't have direct access to the adjacency matrix.



**My Solution: brute force**

```java
/* The knows API is defined in the parent class Relation.
      boolean knows(int a, int b); */

public class Solution extends Relation {
    public int findCelebrity(int n) {
        int[] k = new int[n];
        for(int i = 0; i < n; i++)
        {
            for(int j = 0; j < n; j++)
            {
                if(knows(i,j))
                {
                 k[j]++;   
                }
            }
        }
        for(int i = 0; i < k.length; i++)
        {
            if(k[i] == k.length)
            {
                for(int j = 0; j < k.length;j++)
                {
                    if(j == i)
                        continue;
                    if(knows(i,j))
                        return-1;
                }
                return i;
            }
        }
        return -1;
    }
}
```

**Solution 2: find candidate**

In the first loop, we find the candidate value to simplify the algorithm. In this question, we can only find one candidate because if we find 2 candidate which means they do not know each other. That means all of them are not candidate. The candidate in this loop means this candidate can not knows the right part of candidate. On the left part of candidate means there are no people knows it or it knows some people which means all of these people are not candidate. The second loop is to verify whether the candidate is the value that we want. 

```java
public class Solution extends Relation {
    public int findCelebrity(int n) {
        if(n < 0)
            return -1;
        int candidate = 0;
        for(int i = 0 ; i < n; i ++)
        {
            if(knows(candidate,i))
                candidate = i;
        }
        for(int i = 0; i < n; i++)
        {
            if(candidate!=i && knows(candidate,i) || !knows(i,candidate))
            {
                return -1;
            }
        }
        return candidate;
    }
}
```

This solution also can be simplified. Because in the second loop, we proof that whether candidate knows others from 0 to n. However, **we can only  verify the people from 0 to candidate -1 because we are already know candidate can not know the people from candidate+1 to n by first loop.**

```java
/* The knows API is defined in the parent class Relation.
      boolean knows(int a, int b); */

public class Solution extends Relation {
    public int findCelebrity(int n) {
        if(n < 0)
            return -1;
        int candidate = 0;
        for(int i = 0 ; i < n; i ++)
        {
            if(knows(candidate,i))
                candidate = i;
        }
        for(int i = 0; i < candidate; i++)
        {
            if(knows(candidate,i))
                return -1;
        }
        for(int i = 0; i < n; i++)
        {
            if(!knows(i,candidate))
                return -1;
            // if(candidate!=i && knows(candidate,i) || !knows(i,candidate))
            // {
            //     return -1;
            // }
        }
        return candidate;
    }
}
```