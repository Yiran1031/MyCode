### Question 724: Find Pivot Index
---
Given an array of integers nums, write a method that returns the "pivot" index of this array.
We define the pivot index as the index where the sum of the numbers to the left of the index is equal to the sum of the numbers to the right of the index.
If no such index exists, we should return -1. If there are multiple pivot indexes, you should return the left-most pivot index.
**Example 1:**

```
Input: 
nums = [1, 7, 3, 6, 5, 6]
Output: 3
Explanation: 
The sum of the numbers to the left of index 3 (nums[3] = 6) is equal to the sum of numbers to the right of index 3.
Also, 3 is the first index where this occurs.
```

**Example 2:**

```
Input: 
nums = [1, 2, 3]
Output: -1
Explanation: 
There is no index that satisfies the conditions in the problem statement.
```

**Solution 1:**

```java
class Solution {
    public int pivotIndex(int[] nums) {
        int pivot = 0;
        int l_sum = 0;
        if(nums.length == 0)
            return -1;
        int r_sum = -nums[pivot];
        for(int i = 0 ; i < nums.length; i++)
        {
            r_sum = r_sum + nums[i];
        }
        while(pivot < nums.length)
        {
            if(l_sum == r_sum)
            {
                return pivot;
            }else
            {
                l_sum = l_sum + nums[pivot];
                pivot++;
                if(pivot < nums.length){
                    r_sum = r_sum - nums[pivot];
                }
            }
        }
        return -1;
    }
}
```

**Solution 2: more elegant**
```java
class Solution {
    public int pivotIndex(int[] nums) {
        int sum = 0, leftsum = 0;
        for (int x: nums) sum += x;
        for (int i = 0; i < nums.length; ++i) {
            if (leftsum == sum - leftsum - nums[i]) return i;
            leftsum += nums[i];
        }
        return -1;
    }
}
```

**Note:**

There are some trap that need to pay attention to:

- what if the pivot is the last element.
- what if all value in the array are same.
- what if there are multiple pivot.