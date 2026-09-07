## Day 6 Java DSA Quiz — Fixed Sliding Window

Reply like:

```text
1.A
2.B
3.C
...
15.A
```

### 1. Fixed sliding window is mainly useful for:

A. Continuous subarray problems with fixed size  
B. Tree traversal  
C. Git commands  
D. SQL joins

### 2. In Day 6 problem, window size is:

A. Always `k`  
B. Always changing randomly  
C. Always `0`  
D. Always full array

### 3. Problem asks for:

A. Minimum element in array  
B. Maximum sum of continuous subarray of size `k`  
C. Count of duplicates  
D. Sorted array output

### 4. Brute force approach recalculates:

A. Every window sum fully  
B. Only first value  
C. Only duplicate values  
D. Only indexes

### 5. Brute force time complexity is:

A. O(n)  
B. O(n * k)  
C. O(1)  
D. O(log n)

### 6. Optimized sliding window first calculates:

A. Sum of first `k` numbers  
B. Sum of all numbers always  
C. Sorted version of array  
D. HashMap count

### 7. When sliding right, remove:

A. Outgoing left value  
B. Incoming right value  
C. Maximum value only  
D. Target value

### 8. When sliding right, add:

A. Outgoing left value  
B. Incoming right value  
C. Zero always  
D. First value always

### 9. Correct update formula is:

A. `windowSum = windowSum - outgoing + incoming`  
B. `windowSum = outgoing - incoming`  
C. `windowSum = maxSum`  
D. `windowSum = nums.length`

### 10. Optimized time complexity is:

A. O(1)  
B. O(n)  
C. O(n²)  
D. O(log n)

### 11. Optimized space complexity is:

A. O(1)  
B. O(n)  
C. O(k)  
D. O(n²)

### 12. Why is `maxSum = 0` dangerous?

A. It fails when all numbers are negative  
B. It makes array sorted  
C. It changes k  
D. It improves time complexity

### 13. Correct initial `maxSum` should be:

A. `0`  
B. `windowSum` after first k numbers  
C. `nums.length`  
D. `k`

### 14. If `k > nums.length`, we should:

A. Handle as invalid input  
B. Sort array  
C. Return first element always  
D. Ignore k

### 15. 80/20 rule for fixed-size window:

A. Subtract outgoing left and add incoming right  
B. Use recursion  
C. Use stack  
D. Use binary search
