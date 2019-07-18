### Question 498 : Diagonal Traverse
---

Given a matrix of M x N elements (M rows, N columns), return all elements of the matrix in diagonal order as shown in the below image.

 

**Example:**

```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]

Output:  [1,2,4,7,5,3,6,8,9]

Explanation:
```

 

**Note:**

The total number of elements of the given matrix will not exceed 10,000.

**Solution : **

```java
class Solution {
    public int[] findDiagonalOrder(int[][] matrix) {
        if(matrix.length == 0 || matrix[0].length == 0)
            return new int[0];
        int i = 0;
        int j = 0;
        int n = 0;
        int[] re = new int[ matrix.length*matrix[0].length];
        while(n < re.length)
        {
            re[n] = matrix[i][j];
            if((i+j) % 2 == 0)
            {
                if(j == matrix[0].length-1) 
                {
                    i++;
                }
                else if( i == 0) 
                {
                    j++;
                } 
                else
                {
                    i--;
                    j++;
                }
                n++;
            }else if((i+j) % 2 == 1)
            {
                if( i == matrix.length - 1)
                {
                    j++;
                }else if(j == 0)
                {
                    i++;
                } else
                {
                    i++;
                    j--;
                }
                n++;
            }
        }
        return re;
    }
}
```

