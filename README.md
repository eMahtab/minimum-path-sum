# Minimum path sum
## https://leetcode.com/problems/minimum-path-sum

# Implementation 1
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
