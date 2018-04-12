### Thief's Knapsack Problem

Code Explanation: 
- Make a table using a range method, to make a large array of arrays. 
- Iterating through items, and then iterating through weights nested inside that. 

### Dynamic Programing:
- Recursion or iteration with memoization 
- Identify repeated work and memoize it
- n fibonacci is a good example
- start by thinking what if we have no items,
- what is our max value with a weight of 5
- table considers what if we had 0 items, 1 item, etc
- what if our max weight was 0, 1 , 2, 3, 4
- Algorithm
  * does item fit?
  * waht is the max value if we don't include item (check previous row)
  * what is the max value if we do include the item (value of item + previous max value @ (max weight - item weight))
