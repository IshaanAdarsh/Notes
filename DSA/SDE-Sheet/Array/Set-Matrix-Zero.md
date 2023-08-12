# Set Matrix Zero:
**Problem Statement:** Given a matrix if an element in the matrix is 0, you will have to set its entire column and row to 0 and then return the matrix.

## Brute Force Approach:
### Approach:
- The steps are the following:
  - First, we will use two loops(nested loops) to traverse all the matrix cells.
  - If any cell (i,j) contains the value 0, we will mark all cells in row i and column j with -1 except those which contain 0.
  - We will perform step 2 for every cell containing 0.
  - Finally, we will mark all the cells containing -1 with 0.

