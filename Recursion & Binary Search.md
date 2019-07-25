### Recursion & Binary Search
---



Recursion: Definition:

- Function calls itself
- Boil down a big problem to smaller one (size n depends on size n-1, or n-2 or …. n/2)
- Implementation
  - Base case: smallest problem to solve
  - Recursive rule: how to make problem smaller

Binary Search : 

- Principles:
  - guarantee that the search space(that possibly contains the target to find) decrease over time(after each iteration).
  - We mush guarantee that the target cannot be ruled out accidentally.

```java
public int binarySearch(int[] array, int target)
{
  if(array == null || array.length == 0)
  {
    return -1;
  }
  
  int left = 0, right = array.length - 1;
  while(left <= right)
  {
    int mid = left + (right - left)/2;
    if(array[mid] == target){
      return mid;
    }else if(array[mid] > target)
    {
      // what if right = mid?
      right = mid - 1;
    }else{
      left = mid + 1;
    }
  }
  
  return -1;
}
```

