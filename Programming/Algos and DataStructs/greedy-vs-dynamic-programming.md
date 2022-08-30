# Greedy vs Dynamic Programming

## Greedy
- A **greedy algorithm** is an algorithmic paradigm that builds up a solution piece by piece, always choosing the next piece that offers the most obvious and immediate benefit.
- So the problems where choosing locally optimal also leads to a global solution are best fit for Greedy.
-e.g Consider the **Fractional Knapsack** Problem.
- the local optimal strategy is to choose the item that has maximum value vs weight ratio. This strategy also leads to global optimal solution because we allowed taking fractions of an item.

## Dynamic
- is mainly an optimization over plain recursion.
- Whereever we see a recursive solution that has repeated calls for the same inputs, we can optimize it using **Dynamic Programming**
- The idea is to simply store the results of subproblems so that we do not have to re-compute them when needed later.
- This simple optimization reduces time complexities from exponential to polynomial
- e.g if we write a simple recursive solution for **Fibonacci Numbers** we get exponential time complexity and if we optimize it by storing solutions of subproblems, time complexity reduces to linear.


