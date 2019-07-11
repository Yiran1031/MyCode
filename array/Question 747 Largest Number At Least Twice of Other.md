###  Question 747: Largest Number At Least Twice of Other
---
In a given integer array nums, there is always exactly one largest element.
Find whether the largest element in the array is at least twice as much as every other number in the array.
If it is, return the index of the largest element, otherwise return -1.
**Example 1:**
```
Input: nums = [3, 6, 1, 0]
Output: 1
Explanation: 6 is the largest integer, and for every other number in the array x,
6 is more than twice as big as x.  The index of value 6 is 1, so we return 1.
```
**Example 2:**
```
Input: nums = [1, 2, 3, 4]
Output: -1
Explanation: 4 isn't at least as big as twice the value of 3, so we return -1.
```

**Original Solution:**

```java
class Solution {
    public int dominantIndex(int[] nums) {
        int max = -1;
        int s_max = -1;
        int index = -1;
        if(nums.length == 0)
            return -1;
        for(int i = 0; i < nums.length; i++)
        {
            if(max < nums[i])
            {
                //s_max = max;
                max = nums[i];  
                index = i;
            }
        }
        for(int i = 0; i < nums.length; i++)
        {
            if(nums[i] < max)
            {
                if(s_max < nums[i])
                    s_max = nums[i];
            }
        }
        if(s_max*2 > max)
            index = -1;
        return index;
    }
}
```

**Advanced Solution: less memory**
```java
class Solution {
    public int dominantIndex(int[] nums) {
        int max = 0;
        int index = 0;
        if(nums.length == 0)
            return -1;
        for(int i = 0; i < nums.length; i++)
        {
            if(max < nums[i])
            {
                //s_max = max;
                max = nums[i];  
                index = i;
            }
        }
        for(int i = 0; i < nums.length; i++)
        {
            if(nums[i]!=nums[index] && nums[i]*2>nums[index])
            {
                return -1;
            }
        }

        return index;
    }
}
```

