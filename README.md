# Day-26-Matrix-Chain-Multiplication.
Here's Python Program for Matrix Chain Multiplication. Day 26 of Day 365.
 Goal
Matrix Chain Multiplication aims to find the most efficient way to multiply a given sequence of matrices. Unlike normal matrix multiplication, which is straightforward, this problem focuses on minimizing the computational cost (number of scalar multiplications).

 Example Scenario
Suppose we have matrices A, B, C, and D with the following dimensions:
- A: 10x20
- B: 20x30
- C: 30x40
- D: 40x30

 Steps:

1. Define the Problem: 
   - We have matrices A1, A2, ..., An to multiply.
   - The order of multiplication is fixed, but we want to find the optimal way to parenthesize the product.

2. Understand Matrix Multiplication Cost:
   - The cost of multiplying a p×q matrix by a q×r matrix is p*q*r scalar multiplications.

3. Dynamic Programming Approach:
   - Initialization: Create a table `m` where `m[i][j]` will represent the minimum number of scalar multiplications needed to compute the product of matrices from Ai to Aj.
   - Base Case: `m[i][i] = 0` for all i because the cost of multiplying a single matrix is zero.

4. Fill the Table:
   - Length of the Chain: Start with chains of length 2, then 3, and so on, up to the length `n`.
   - For each chain length `L` from 2 to `n`:
     - For each starting point `i` from 1 to `n-L+1`:
       - Set the endpoint `j` as `i + L - 1`.
       - Set `m[i][j]` to a large value (infinity).
       - Compute the minimum cost of multiplying matrices Ai to Aj by trying different points `k` to split the product:
         - Cost `q = m[i][k] + m[k+1][j] + p[i-1]*p[k]*p[j]`.
         - Update `m[i][j]` with the minimum value of `q`.

5. Example Calculation:
   - Let's multiply matrices A (10x20), B (20x30), C (30x40), and D (40x30):
     - Chain of length 2: 
       - `m[1][2] = 10*20*30 = 6000`
       - `m[2][3] = 20*30*40 = 24000`
       - `m[3][4] = 30*40*30 = 36000`
     - Chain of length 3:
       - `m[1][3]`: Try `k=1` and `k=2`:
         - Cost with `k=1`: `m[1][1] + m[2][3] + 10*20*40 = 0 + 24000 + 8000 = 32000`
         - Cost with `k=2`: `m[1][2] + m[3][3] + 10*30*40 = 6000 + 0 + 12000 = 18000`
         - So, `m[1][3] = 18000`
       - `m[2][4]`: Try `k=2` and `k=3`:
         - Cost with `k=2`: `m[2][2] + m[3][4] + 20*30*30 = 0 + 36000 + 18000 = 54000`
         - Cost with `k=3`: `m[2][3] + m[4][4] + 20*40*30 = 24000 + 0 + 24000 = 48000`
         - So, `m[2][4] = 48000`
     - Chain of length 4:
       - `m[1][4]`: Try `k=1`, `k=2`, and `k=3`:
         - Cost with `k=1`: `m[1][1] + m[2][4] + 10*20*30 = 0 + 48000 + 6000 = 54000`
         - Cost with `k=2`: `m[1][2] + m[3][4] + 10*30*30 = 6000 + 36000 + 9000 = 51000`
         - Cost with `k=3`: `m[1][3] + m[4][4] + 10*40*30 = 18000 + 0 + 12000 = 30000`
         - So, `m[1][4] = 30000`

The final minimum cost to multiply matrices A, B, C, and D is 30,000 scalar multiplications, and we can deduce the optimal order from the `m` table and the splits `k` chosen.

 Conclusion
Matrix Chain Multiplication helps find the most efficient order to multiply a series of matrices by minimizing the computational cost. Using dynamic programming, we break down the problem into smaller subproblems and solve them efficiently.
