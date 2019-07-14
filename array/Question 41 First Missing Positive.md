###  Question 41: First Missing Positive

hard

---
Given an unsorted integer array, find the smallest missing positive integer.
Example:

```
Input: [1,2,0]
Output: 3
```
```
Input: [3,4,-1,1]
Output: 2
```
```
Input: [7,8,9,11,12]
Output: 1
```

**Solution 1: simple way**

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        Arrays.sort(nums);
        int target = 1;
        for(int i = 0; i < nums.length; i++)
        {
            if(nums[i] > target)
                return target;
            if(nums[i] == target)
                target++;
        }
        return target;
    }
}
```

**Solution 2 : Index as a hash key**

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        //check if i exist
        int contains = 0;
        for(int i = 0; i < nums.length; i++)
        {
            if(nums[i] == 1)
            {
                contains = 1;
                break;
            }
        }
        if(contains == 0)
            return 1;
        // include 1 and only have 1 element.
        if(nums.length == 1)
            return 2;
        
        
        // data clean up;
        for(int i = 0; i < nums.length; i++)
        {
            if(nums[i] <=0 || nums[i] > nums.length)
                nums[i] = 1;
        }
        
        for(int i = 0; i < nums.length; i++)
        {
            int a = Math.abs(nums[i]);
            //using index 0 to represent index n because we can not get n in array.
            if(a == nums.length)
                nums[0] = - Math.abs(nums[0]);
            else
                nums[a] = - Math.abs(nums[a]);
        }
        
        for(int i = 1 ; i < nums.length; i++)
        {
            if(nums[i] > 0)
                return i;
        }
        if(nums[0] > 0)
            return nums.length;
        return nums.length+1;
    }
}
```

