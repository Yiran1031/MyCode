###  Question 26： Remove Duplicates from Sorted Array
---
Given a sorted array *nums* , remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array** in-place with O(1) extra memory.

**Example 1:**
```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**
```
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

**My Solution:**

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int n = 1;
        int i = 0;
        while(n < nums.length){
            if(nums[i] < nums[n])
            {
                i++;
                nums[i] = nums[n];   
            }else
            {
                n++;
            }
        }
        return i+1;
    }
}
```

**Note:** This question is similar with question 27. In order to deal with this question, we need two point **n** and **i** to operate array. The variable **i** means there are **i** nums has been selected. The variable **n** start with i + 1 and move to right 1 index when nums[i] >= nums[n].If nums[i] < nums[n], we copy the value of nums[n] to nums[i+1] and make i plus 1. Because the array has been sorted. The arrays less than **i** is what we want.

