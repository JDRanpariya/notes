A Modern computer can perform 10^8 operations per sec.

Therefore, loop for adding N natural numbers will take N additions and so for 10^10
it will take 100 sec. Where as N*(N+1)/2 is just 3 operations.

Fundamental Idea of Algorithm Analysis
 - count the no. of steps your program takes to execute and try to figure out how it grows as your input becomes larger.
 - we dump the exact formula and try to get some idea of how the algorithm performs as the input size increases.
 
Big-O Notation
 - simplified analysis of an algorithm's efficiency
 - complexity in terms of input size, Notation
 - Machine independent
 - basic computer steps
 - Both time and space
 - types of measurement
   - worst-case (this is what we use)
   - best-case
   - average-case
 - general rules
  - ingnore constants (5n -> O(n))
  - certain terms "dominate" others
      - O(1) < O(logn) < O(n) < O(nlogn) < O(n^2) < O(2^n) < O(n!)
      - [Big-O cheatsheet](https://www.bigocheatsheet.com/)

# constant time 
 - x = 5 + (15*20);
 - independent of input size, N
 - O(1)

## example 1
x = 5 + (15*20);
y = 15 - 2;
print x+y;

total time = O(1) + O(1) + O(1) = 3 * O(1) = O(1)

# linear time 
 - for x in range(0,n):
     print x; // O(1)
 - total time = N * O(1) = O(N)

# Quadratic time O(N^2)
for x in range(0,n):
  for y in range(0,n):
    print x*y; // O(1)

total time = O(N^2)

## Note: if O(1), O(n) and O(n^2) is there gratest will be the ans.

# Big-O for conditionals

if x>0:
  // O(1)
else if x<0:
  // O(logn)
else:
  // O(n^2)

total time will be O(n^2)

# References
- [Complexity and Big-O Notation](http://pages.cs.wisc.edu/~paton/readings/Complexity/#bigO)

