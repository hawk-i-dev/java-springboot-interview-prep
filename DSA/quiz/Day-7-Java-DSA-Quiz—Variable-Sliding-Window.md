## Day 7 Java DSA Quiz — Variable Sliding Window

Reply like:

```text
1.A
2.B
3.C
...
15.A
```

### 1. Variable sliding window means:

A. Window size can expand and shrink  
B. Window size is always fixed  
C. Array is sorted first  
D. Stack is used always

### 2. Day 7 problem asks for:

A. Longest substring without repeating characters  
B. Maximum sum of fixed size k  
C. Valid parentheses  
D. Contains duplicate

### 3. Substring means:

A. Continuous part of a string  
B. Characters selected in any order  
C. Sorted characters only  
D. Only duplicate characters

### 4. Valid window for this problem means:

A. No duplicate characters  
B. Only lowercase letters  
C. Sorted characters  
D. Window size exactly k

### 5. HashSet version stores:

A. Characters currently inside the window  
B. Character indexes only  
C. All previous strings  
D. Sorted characters

### 6. `left` represents:

A. Start of current window  
B. End of string always  
C. Maximum length  
D. Duplicate count

### 7. `right` represents:

A. New/current character position  
B. Start of current window  
C. Length of answer  
D. Last removed character

### 8. If current character already exists in `seen`, we should:

A. Shrink from left until duplicate is removed  
B. Return false  
C. Sort the string  
D. Clear the whole string

### 9. In HashSet version, why use `while` instead of only `if`?

A. Multiple removals from left may be needed  
B. `if` cannot check HashSet  
C. `while` makes code O(1)  
D. Strings require while only

### 10. When should `maxLength` be updated?

A. After the window becomes valid  
B. Before removing duplicates  
C. Before the loop starts only  
D. Only when string ends

### 11. For `"abcabcbb"`, answer is:

A. 1  
B. 2  
C. 3  
D. 4

### 12. For `"bbbbb"`, answer is:

A. 0  
B. 1  
C. 5  
D. 2

### 13. In HashMap optimized version, map stores:

A. character → last seen index  
B. index → character  
C. character → count only  
D. number → index

### 14. Why check `lastSeen.get(ch) >= left`?

A. To avoid moving left backward  
B. To sort the map  
C. To remove all duplicates  
D. To make time O(n²)

### 15. Time and space complexity are:

A. Time O(n), Space O(k)  
B. Time O(n²), Space O(1)  
C. Time O(log n), Space O(n)  
D. Time O(1), Space O(1)
