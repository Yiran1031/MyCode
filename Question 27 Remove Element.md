### Question 27: Remove Element
---
Given an array nums and a value *val* , remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this modifying the input array in-place with O(1) extra memory.

The other of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example1:**

```
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

Note that the order of those five elements can be arbitrary.
```



**Solution 1:**

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0;
        for(int j = 0; j < nums.length; j++)
        {
            if(nums[j] != val)
            {
                nums[i] = nums[j];
                i++;
            }
        }
        return i;
    }
}
```

**Solution 2:** remove some unnecessary copy when val is rare.

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int n = nums.length;
        int i = 0;
        while(i<n)
        {
            if(nums[i] == val)
            {
                nums[i] = nums[n-1];
                n--;
            }else
            {
                i++;
            }
        }
        return n;
    }
}
```

**Note:**

Solution 2 is change value from the end of array. All value that index lower than i will target value. The value that index higher than n will be considered at val. n is the length of result after iteration. This solution only exchange the val that **only need to delete.**

