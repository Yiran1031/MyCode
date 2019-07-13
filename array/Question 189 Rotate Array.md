### Question 189: Rotate Array
---
Given an array, rotate the array to the right by k steps, where k is non-negative.
**Example 1:**
```
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```
**Example 2:**

```
Input: [-1,-100,3,99] and k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

**Note:**
- Try to come up as many solution as you can, there are at least 3 different ways to solve this problem.
- Could you do it in-place with O(1) extra space ?



**Solution 1:** 

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int[] temp  = new int[nums.length];
        for(int m = 0 ; m < nums.length; m++)
        {
            temp[m] = nums[m];
        }
        for(int i = 0; i < k; i++)
        {
            nums[0] = temp[temp.length - 1];
            for(int j = 0; j < nums.length-1;j++)
            {
                nums[j+1] = temp[j];
            }
            for(int m = 0 ; m < nums.length; m++)
            {
                temp[m] = nums[m];
            }
        }
    }
}
```

**Solution 2:  with out another array**

```java
class Solution {
    public void rotate(int[] nums, int k) {
        for(int i = 0; i < k; i++)
        {
            int temp = nums[nums.length-1];
            nums[nums.length-1] = nums[0];
            nums[0] = temp;
            for(int j = 1 ; j < nums.length; j++)
            {
                int t = nums[nums.length-1];
                nums[nums.length-1] = nums[j];
                nums[j] = t;
            }
        }
    }
}
```

**Solution 3: O(n) time complexity**

```java
class Solution {
    public void rotate(int[] nums, int k) {
        k = nums.length - (k%nums.length);
        int[] temp1 = new int[k];
        int[] temp2 = new int[nums.length-k];
        for(int i = 0; i < nums.length; i++)
        {
            if(i < k)
            {
                temp1[i] = nums[i];
            }else{
                temp2[i-k] = nums[i];
            }
        }
        for(int j = 0; j < nums.length; j++)
        {
            if(j < nums.length-k)
            {
                nums[j] = temp2[j];
            }else
            {
                nums[j] = temp1[j-(nums.length-k)];
            }
        }
     }
}
```

Solution 4: Using Cyclic Replacements

```java
public class Solution {
    public void rotate(int[] nums, int k) {
        k = k%nums.length;
        int i = 0;
        int previous = nums[0];
        while( i < k )
        {
            int j = i;
            while(j < nums.length)
            {
                j = j+k;
                if(j >= nums.length)
                {
                    int temp = nums[j-nums.length];
                    nums[j-nums.length] = previous;
                    previous = temp;
                }else
                {
                    int temp = nums[j];
                    nums[j] = previous;
                    previous = temp;
                }
            }
            i = i + 1;
        }

    }
}
```

