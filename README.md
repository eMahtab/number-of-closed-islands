# Number of closed islands
## https://leetcode.com/problems/number-of-closed-islands

Given a 2D grid consists of 0s (land) and 1s (water).  An island is a maximal 4-directionally connected group of 0s and a closed island is an island totally (all left, top, right, bottom) surrounded by 1s.

Return the number of closed islands.

![Closed Island](closed-island.png?raw=true "Closed Island")

e.g. For above grid, the number of closed islands is 2.

### Implementation 1 : Mutating the input array , Time : O(rows * columns) , Space : O(rows * columns)

```java
class Solution {
    public int closedIsland(int[][] grid) {
        if(grid == null || grid.length == 0)
            return 0;
        
        int rows = grid.length, columns = grid[0].length, closedIslands = 0;
        
        for(int col = 0; col < columns; col++) {
            if(grid[0][col] == 0)
            traverse(grid, 0, col);
            
            if(grid[rows - 1][col] == 0)
            traverse(grid, rows - 1, col);
        }
        
        for(int row = 0; row < rows; row++) {
            if(grid[row][0] == 0)
            traverse(grid, row, 0);
            
            if(grid[row][columns - 1] == 0)
            traverse(grid, row, columns - 1);
        }
            
        for(int row = 1; row < rows; row++) {
            for(int col = 1; col < columns; col++) {
                if(grid[row][col] == 0) {
                    closedIslands++;
                    traverse(grid, row, col);
                }   
            }
        }
        return  closedIslands;
    }
    
    private void traverse(int[][] grid, int row, int col) {
        if(row < 0 || row >= grid.length || col < 0 || col >= grid[0].length || grid[row][col] != 0)
            return;
        
        grid[row][col]  = '#';
        traverse(grid, row, col + 1);
        traverse(grid, row, col - 1);
        traverse(grid, row - 1, col);
        traverse(grid, row + 1, col);
    }
}
```

### Implementation 2 : Without mutation, Time : O(rows * columns) , Space : O(rows * columns)

```java
class Solution {
    public int closedIsland(int[][] grid) {
        if(grid == null || grid.length == 0)
            return 0;
        
        int rows = grid.length, columns = grid[0].length, closedIslands = 0;
        
        for(int col = 0; col < columns; col++) {
            if(grid[0][col] == 0)
            traverse(grid, 0, col);
            
            if(grid[rows - 1][col] == 0)
            traverse(grid, rows - 1, col);
        }
        
        for(int row = 0; row < rows; row++) {
            if(grid[row][0] == 0)
            traverse(grid, row, 0);
            
            if(grid[row][columns - 1] == 0)
            traverse(grid, row, columns - 1);
        }
            
        for(int row = 1; row < rows; row++) {
            for(int col = 1; col < columns; col++) {
                if(grid[row][col] == 0) {
                    closedIslands++;
                    traverse(grid, row, col);
                }   
            }
        }
        // Revert '#' back to 0
        for(int row = 0; row < rows; row++) {
            for(int col = 0; col < columns; col++) 
                if(grid[row][col] == '#')
                    grid[row][col] = 0;
        }
        return  closedIslands;
    }
    
    private void traverse(int[][] grid, int row, int col) {
        if(row < 0 || row >= grid.length || col < 0 || col >= grid[0].length || grid[row][col] != 0)
            return;
        
        grid[row][col]  = '#';
        traverse(grid, row, col + 1);
        traverse(grid, row, col - 1);
        traverse(grid, row - 1, col);
        traverse(grid, row + 1, col);
    }
}
```

# References :
https://github.com/eMahtab/surrounded-regions
