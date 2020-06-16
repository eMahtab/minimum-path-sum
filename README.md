# Minimum path sum
## https://leetcode.com/problems/minimum-path-sum

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

**Note: You can only move either down or right at any point in time.**
```
Example:

Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]

Output: 7

Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```
# Implementation 1 : Mutating input array , Time : O(rows * columns) , Space : O(1)
```java
class Solution {
    public int minPathSum(int[][] grid) {
        if(grid == null || grid.length == 0)
            return 0;
        int rows = grid.length, columns = grid[0].length;
        for(int col = 1; col < columns; col++) {
            grid[0][col] += grid[0][col-1]; 
        }
        for(int row = 1; row < rows; row++) {
            grid[row][0] += grid[row-1][0];
        }
        for(int row = 1; row < rows; row++) {
            for(int col = 1; col < columns; col++) {
                grid[row][col] += Math.min(grid[row-1][col], grid[row][col-1]);
            }
        }
        return grid[rows-1][columns-1];
    }
}
```

# Implementation 2 : Without Mutation  , Time : O(rows * columns) , Space : O(rows * columns)
```java
class Solution {
    public int minPathSum(int[][] grid) {
        if(grid == null || grid.length == 0)
            return 0;
        int rows = grid.length, columns = grid[0].length;
        int[][] dp = new int[rows][columns];
        dp[0][0] = grid[0][0];
        for(int col = 1; col < columns; col++) {
            dp[0][col] = dp[0][col-1] + grid[0][col]; 
        }
        for(int row = 1; row < rows; row++) {
            dp[row][0] = dp[row-1][0] + grid[row][0];
        }
        for(int row = 1; row < rows; row++) {
            for(int col = 1; col < columns; col++) {
                dp[row][col] = Math.min(dp[row-1][col], dp[row][col-1]) + grid[row][col];
            }
        }
        return dp[rows-1][columns-1];
    }
}
```

# References :
https://github.com/eMahtab/unique-paths
