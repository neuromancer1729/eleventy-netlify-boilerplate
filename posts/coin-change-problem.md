---
title: Coin Change Problem
date: 2019-11-16T15:35:01.326Z
summary: >-
  The change-making problem is a subset of Knapsack problems which addresses the
  question of finding the minimum number of coins (of certain denominations)
  that add up to a given amount of money. Coin change is a general case of the
  same.
tags:
  - interview-questions
  - algorithms
---
## 

Write a function min_coins(cents) return the minumum number of coins to return the principal amount in change. Available denomication Quarters(25), dime(10), nickels(5) and pennies(1)

```
min_coins(31) => 3 [1xQuarter + 1xnickel + 1xpenny]
```

greedy strategy

```
def min_coins(cents):  
  if cents < 1: return 0  
  coins = [25,10,5,1]  
  num_coins = 0  
  for coin in coins:    
    num_coins += cents/coin    
    cents = cents/coin  
  return num_coins  
```

It is a constant time solution which is optimal for the given scenario.

Now, what if there are no nickels in the cash register ? Is it still the optimal solution ?

For example, if cents = 31, and the available denominations are \[25, 10, 1] our greedy code will return 7 (1quarter and 6pennies ) as the answer. But we know that optimal solution is 4 coins (3 dimes and 1 penny).

The most elegant solution I found online was by leetcode user 'hweicdl' as follow

```
def min_coins(cents):  
  coins = [25,10,1]
  d = [0] + [float('inf')]*cents 
  for coin in coins:
    for i in range(coins, cents+1):
      d[i] = min(d[i], d[i-coin]+1)
  return d[-1]   
```

It's a classic bottom up [Dynamic programming](https://www.tutorialspoint.com/data_structures_algorithms/dynamic_programming.htm) solution with O(N) time and constant space complexity.

Note how the entire code requires not a single division or mod operator. 
How crazy is that !!

References

<https://en.wikipedia.org/wiki/Change-making_problem>

<https://leetcode.com/problems/coin-change/solution/>
