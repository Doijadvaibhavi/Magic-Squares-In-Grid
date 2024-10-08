# Magic-Squares-In-Grid

A 3 x 3 magic square is a 3 x 3 grid filled with distinct numbers from 1 to 9 such that each row, column, and both diagonals all have the same sum.

Given a row x col grid of integers, how many 3 x 3 contiguous magic square subgrids are there?

Note: while a magic square can only contain numbers from 1 to 9, grid may contain numbers up to 15.


Example 1:


Input: grid = [[4,3,8,4],[9,5,1,9],[2,7,6,2]]
Output: 1
Explanation: 
The following subgrid is a 3 x 3 magic square:

while this one is not:

In total, there is only one magic square inside the given grid.
Example 2:

Input: grid = [[8]]
Output: 0
 
Constraints:

row == grid.length
col == grid[i].length
1 <= row, col <= 10
0 <= grid[i][j] <= 15

# SOLUTION

1. Institution (Understanding the Problem)
The problem requires identifying all 3x3 subgrids within a given 2D grid that are magic squares. A magic square is defined by specific criteria:

Distinct numbers from 1 to 9: Each number within the 3x3 grid must be unique and between 1 and 9.
Equal row, column, and diagonal sums: All rows, columns, and diagonals must sum to the same value.

2. Approach (Step-by-Step Solution):
   
Step 1: Identify Valid 3x3 Subgrids
Iterate through the 2D grid starting from each possible top-left corner of a 3x3 subgrid.
Ensure that the grid is large enough to contain at least one 3x3 subgrid (i.e., it should be at least 3x3).
Step 2: Check for Magic Square Properties
For each 3x3 subgrid, check if all the numbers are distinct and within the range of 1 to 9.
Verify that the sums of all rows, columns, and diagonals are equal.
Step 3: Count the Valid Magic Squares
Maintain a count of how many valid 3x3 magic squares are found.

* Example Approach
Loop through the grid:

Consider every possible 3x3 subgrid starting point (i, j) within the grid.
Check the distinctness and range:

Ensure the numbers within the subgrid are unique and between 1 to 9.
Check the row, column, and diagonal sums:

Calculate and compare the sum of each row, each column, and both diagonals.
Increment the counter:

If the subgrid satisfies all the conditions, increase the count of magic squares.

Institution Recap:

Grid Exploration: By iterating through each possible starting point for a 3x3 subgrid, we ensure that all potential magic squares are checked.
Magic Square Validation: Each 3x3 grid is validated against the magic square criteria to count valid magic squares.

* Conclusion
The approach is systematic and ensures that every 3x3 subgrid is evaluated efficiently. The solution considers both the structural properties of magic squares and the constraints of the problem (e.g., number uniqueness and range). This institutional and approach framework guides the problem-solving process from understanding to implementation.

* Complexity
  
Time complexity: O(N^2)

Space complexity: O(1)

# JAVA CODE

class Solution {

    public int numMagicSquaresInside(int[][] grid) {
    
       int count = 0;
       
        int rows = grid.length;
        
        int cols = grid[0].length;

        for (int i = 0; i <= rows - 3; i++) {
        
            for (int j = 0; j <= cols - 3; j++) {
            
                if (isMagicSquare(grid, i, j)) {
                
                    count++;
                }
            }
        }

        return count;   
    }

    private boolean isMagicSquare(int[][] grid, int i, int j) {
    
        // Check for distinct numbers from 1 to 9
        
        boolean[] seen = new boolean[10];
        
        for (int x = 0; x < 3; x++) {
        
            for (int y = 0; y < 3; y++) {
            
                int num = grid[i + x][j + y];
                
                if (num < 1 || num > 9 || seen[num]) return false;
                
                seen[num] = true;
            }
        }

        int sum = grid[i][j] + grid[i][j+1] + grid[i][j+2];  // First row sum
        
        // Check rows
        
        for (int x = 0; x < 3; x++) {
        
            if (sum != grid[i + x][j] + grid[i + x][j + 1] + grid[i + x][j + 2]) return false;
        }

        // Check columns
        
        for (int y = 0; y < 3; y++) {
        
            if (sum != grid[i][j + y] + grid[i + 1][j + y] + grid[i + 2][j + y]) return false;
        }

        // Check diagonals
        
        if (sum != grid[i][j] + grid[i+1][j+1] + grid[i+2][j+2]) return false;
        
        if (sum != grid[i+2][j] + grid[i+1][j+1] + grid[i][j+2]) return false;

        return true;
    }
}

