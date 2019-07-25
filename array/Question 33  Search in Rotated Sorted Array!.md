### Question 33 : Search in Rotated Sorted Array!
---

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`).

You are given a target value to search. If found in the array return its index, otherwise return `-1`.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

**Example 1:**

```java
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

**Example 2:**

```java
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

**Solution : Binary Search**

```java
class Solution {
    public int search(int[] nums, int target) {
        //int mid = 0;
        if(nums == null || nums.length == 0)
            return -1;
        int add = findIndex(nums);
        int left = 0;
        int right = nums.length - 1;
        int len = nums.length;
        if(add == -1)
        {
            add = 0;
        }
            //(nums.length - 1 + add)%nums.length;
        while(left <= right)
        {
            int mid = left + (right - left)/2;
            if(nums[(mid+add) % len] == target)
                return (mid + add)%len;
            else if(nums[(mid+add) % len] > target)
            {
                right = mid - 1;
            }else if(nums[(mid+add) % len] < target)
                left = mid + 1;
        }
        return -1;
        
    }
  // use binary search to find pivot
    public int findIndex(int[] nums)
    {
        int left = 0, right = nums.length - 1;
        int t = nums[0];
        if(nums[left] <= nums[right])
            return -1;
        while(left <= right)
        {
            int mid = left + (right - left)/2;
            if(nums[mid] >= t && nums[mid+1] < t) 
            {
                return mid+1;
            }else if(nums[mid] < t && nums[mid-1] >= t)
            {
                return mid;   
            }
            else if(nums[mid] < t)
            {
                right = mid - 1;
            }else if(nums[mid] > t)
            {
                left = mid + 1;
            }
        }
        return -1;
    }
}
```

