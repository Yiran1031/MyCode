###  Question 15. 3Sum
---
Given an array ``nums`` of **n** integers, are there elements a, b, c in ``nums`` such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

**note:** The solution set must not contain duplicate triplets.

Example:

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```



**Solution:**

```
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        
        List<List<Integer>> result = new ArrayList<>();
        if(nums.length<3)
            return result;
        Arrays.sort(nums);
        
        for(int i = 0; i <= nums.length-1 ;i++)
        {
            int left = i + 1;
            int right = nums.length - 1;
            if(i>=1 && nums[i] == nums[i-1])
                 continue;
            while(left < right)
            {
                int sum = nums[i] + nums[left] + nums[right];
                if(sum == 0)
                {
                    // List<Integer> temp = new ArrayList<Integer>();
                    // temp.add(nums[left]);
                    // temp.add(nums[i]);
                    // temp.add(nums[right]);
                    result.add(Arrays.asList(nums[i],nums[left],nums[right]));
                    
                    left++;
                    right--;
                    
                    
                    while(left < right && nums[left] == nums[left-1])
                        left++;
                    while(left < right && nums[right] == nums[right+1])
                        right--;
                    
                }else if(sum < 0)
                {
                    left++;
                }else
                {
                    right--;
                }
            }
        }
        return result;  
    }
}
```