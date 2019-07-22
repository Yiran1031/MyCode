### Question 119 : Pascal's Triangle II
---

Given a non-negative index *k* where *k* ≤ 33, return the *k*th index row of the Pascal's triangle.

Note that the row index starts from 0.

![img](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)
In Pascal's triangle, each number is the sum of the two numbers directly above it.

**Example:**

```
Input: 3
Output: [1,3,3,1]
```

**Follow up:**

Could you optimize your algorithm to use only *O*(*k*) extra space?

**Solution 1: use 2-d Array and dynamic programming **

```java
/*
* use a dynamic 2-d array to store result;
* use 2 1-d array to sotre a row information
* compute all value in pascal's Trangle
*/
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<List<Integer>> re = new ArrayList<List<Integer>>();
        List<Integer> pre = null,row = null;
        for(int i = 0; i <= rowIndex; i++)
        {
            row = new ArrayList<Integer>();
            for(int j = 0; j <= i; j++)
            {
                if(j == 0 || i == j)
                {
                    row.add(1);
                }else
                {
                    row.add(pre.get(j-1) + pre.get(j));
                }
            }
            re.add(row);
            pre = row;
        }
        return re.get(rowIndex);
    }
}
```

**Solution 2 : use a 1-d Array to optimize solution 1 **

```java
class Solution {
public List<Integer> getRow(int rowIndex) {
    List<Integer> res = new ArrayList<Integer>();
    for(int i = 0;i<rowIndex+1;i++) {
      //inilize all value equals 1 in array
    		res.add(1);
      //calculate each value;
    		for(int j=i-1;j>0;j--) {
    			res.set(j, res.get(j-1)+res.get(j));
    		}
    }
    return res;
}
}
```

 

 **Solution 3 : Formula : n! / (k!(n - k)!) **

```java
class Solution {
public List<Integer> getRow(int rowIndex)
{
  List<Integer> result = new ArrayList<>();
	int rowSize = rowIndex + 1;
  
  for(int k = 0; k < rowSize; k++)
  {
    int num;
    int halfSize = rowSize /2 + rowSize % 2;
    
    if(k < halfSize)
    {
      num = combination(rowIndex, k);
    }else 
    {
      num = result.get(2 * halfSize - k - 1 - rowSize % 2);
    }
    result.add(num);
  }
  return result;
}

int combination(int n , int k)
{
  int i = Math.max(k, n - k + 1);
  int n1 = n;
  int j = 1;
  int n2 = Math.min(k, n - k);
  double numerator = 1;
  double denominator = 1;
  while( i <= n1 || j <= n2)
  {
    while(i <= n1 && Integer.MAX_VALUE / j >= denominator)
    {
      numerator *= i;
      i++;
    }
    while(j <= n2 && Integer.MAX_VALUE / j >= denominator)
    {
      denominator *= j;
      j++;
    }
    
    numerator = numerator / denominator;
    denominator = 1;
  }
  
  return (int) Math.round(numerator / denominator);
}
}
```

