###  Question 11:  Container With Most Water
---
Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note**:You may not slant the container and n is at least 2.

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

Input: [1,8,6,2,5,4,8,3,7]

Output: 49

**Solution 1: Brute force**

```java
class Solution {
    public int maxArea(int[] height) {
        int result = 0;
        for(int i = 0; i < height.length;i++)
        {
            for(int j = i; j < height.length;j++)
            {
                int temp = height[i] < height[j]? height[i] : height[j];
                int r = temp*Math.abs(i-j);
                if(result < r)
                    result = r;
            }            
        }
        return result;
    }
}
```

Solution 2:

```java
class Solution {
    public int maxArea(int[] height) {
        int maxarea = 0,l = 0, r = height.length-1;
        while(l<r)
        {
            maxarea = Math.max(maxarea,Math.min(height[l],height[r])*(r-l));
            if(height[l]<height[r])
                l++;
            else
                r--;
        }
        return maxarea;
    }
}
```

