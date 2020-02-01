# Dynamic Programming

## Definition of DP problems
* Overlapping subproblems: A problem can be broken down into sub-problems, and sub-problems can be broken down into similar and smaller sub-problems.
* Optimum structural property: Most of classical DP problems satisfy this. A given problems has Optimal Substructure Property if optimal solution of the given problem can be obtained by using optimal solutions of its subproblems.

## Step 1: identify DP problem
* Typically, all the problems that require to maximize or minimize certain quantity or counting problems that say to count the arrangements under certain condition or certain probability problems can be solved by using Dynamic Programming.
* All dynamic programming problems satisfy the overlapping subproblems property and most of the classic dynamic problems also satisfy the optimal substructure property.

## Step 2: define state
* A state can be defined as the set of parameters that can uniquely identify a certain position or standing in the given problem. This set of parameters should be as small as possible to reduce state space.

## Step 3 : Formulating a relation among the states
* Find how a sub-problem can be solved by the result of its smaller sub-problems.

## Step 4 : Adding memoization or tabulation for the state
* Improve complexity by storing sub-problem results and removing repeated calculation.

## Tabulation vs Memorization [1]
* Tabulation: 
    * Start from the smallest subproblem, and compute larger subproblems based on small subproblem results.
    * For example, calculate dp[0], dp[1] .... and finally dp[n].
* Memorization:
    * Start from the largest subproblem and recursively calculate smaller subproblems.
    * For example, dp[n] = transition(dp[n - 1]), if dp[n - 1] is not already calculated, then calculate dp[n - 1] first.
    * In this method, we usually initiate the entire dp table with a special value (e.g. -1), so we know the result is not computed yet.

Reference:
* https://www.geeksforgeeks.org/solve-dynamic-programming-problem/
* https://www.geeksforgeeks.org/dynamic-programming/
* https://leetcode.com/tag/dynamic-programming/
* https://www.geeksforgeeks.org/tabulation-vs-memoization/