Assuming you mean **Day 5 Java DSA**.

# Day 5 Java DSA — Sorted Array Two Pointers + Two Sum II

## 1. Concept

Problem:

```text
Find two numbers in a sorted array whose sum equals target.
Return their indexes.
```

Example:

```java
numbers = [2, 7, 11, 15]
target = 9
```

Output:

```java
[0, 1]
```

Because:

```text
numbers[0] + numbers[1] = 2 + 7 = 9
```

## 2. Feynman Explanation

Imagine numbers are standing in sorted order.

```text
2   7   11   15
```

One person stands at the smallest number.

One person stands at the biggest number.

```text
left  = smallest
right = biggest
```

Add them.

```text
If sum is too small → move left forward
If sum is too big   → move right backward
If sum matches      → answer found
```

This works only because the array is sorted.

## 3. 80/20 Rule

Remember this:

```text
Sorted array + pair sum = two pointers.
```

If the array is unsorted:

```text
Use HashMap
```

If the array is sorted:

```text
Use two pointers
```

## 4. Brute Force Approach

Check every pair.

```java
public static int[] twoSumSortedBruteForce(int[] numbers, int target) {
    for (int i = 0; i < numbers.length; i++) {
        for (int j = i + 1; j < numbers.length; j++) {
            if (numbers[i] + numbers[j] == target) {
                return new int[] {i, j};
            }
        }
    }

    return new int[] {};
}
```

Complexity:

```text
Time: O(n²)
Space: O(1)
```

## 5. Optimized Two-Pointer Approach

Use:

```java
left = 0;
right = numbers.length - 1;
```

Decision:

```text
sum == target → return indexes
sum < target  → move left forward
sum > target  → move right backward
```

## 6. Java Code

Create file:

```text
Day05TwoSumSorted.java
```

Code:

```java
package dsa.practice;

import java.util.Arrays;

public class Day05TwoSumSorted {

    public static void main(String[] args) {
        System.out.println(Arrays.toString(twoSumSortedBruteForce(new int[] {2, 7, 11, 15}, 9))); // [0, 1]

        System.out.println(Arrays.toString(twoSumSortedTwoPointers(new int[] {2, 7, 11, 15}, 9)));   // [0, 1]
        System.out.println(Arrays.toString(twoSumSortedTwoPointers(new int[] {1, 2, 3, 4, 6}, 6)));  // [1, 3]
        System.out.println(Arrays.toString(twoSumSortedTwoPointers(new int[] {1, 3, 4, 5, 7}, 12))); // [3, 4]
        System.out.println(Arrays.toString(twoSumSortedTwoPointers(new int[] {1, 2, 3}, 10)));       // []
    }

    public static int[] twoSumSortedBruteForce(int[] numbers, int target) {
        for (int i = 0; i < numbers.length; i++) {
            for (int j = i + 1; j < numbers.length; j++) {
                if (numbers[i] + numbers[j] == target) {
                    return new int[] {i, j};
                }
            }
        }

        return new int[] {};
    }

    public static int[] twoSumSortedTwoPointers(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;

        while (left < right) {
            int currentSum = numbers[left] + numbers[right];

            if (currentSum == target) {
                return new int[] {left, right};
            }

            if (currentSum < target) {
                left++;
            } else {
                right--;
            }
        }

        return new int[] {};
    }
}
```

## 7. Dry Run

Input:

```java
numbers = [1, 2, 3, 4, 6]
target = 6
```

Start:

```text
left = 0 → value 1
right = 4 → value 6
sum = 7
```

`7` is too big.

```text
Move right backward
```

Now:

```text
left = 0 → value 1
right = 3 → value 4
sum = 5
```

`5` is too small.

```text
Move left forward
```

Now:

```text
left = 1 → value 2
right = 3 → value 4
sum = 6
```

Answer:

```java
[1, 3]
```

## 8. Complexity

Optimized approach:

```text
Time Complexity: O(n)
```

Because each pointer moves at most once across the array.

```text
Space Complexity: O(1)
```

Because we only use variables:

```text
left
right
currentSum
```

## 9. Important Java Interview Note

LeetCode **Two Sum II** usually asks for **1-based indexes**.

For LeetCode version, return:

```java
return new int[] {left + 1, right + 1};
```

For our learning track, we are using normal Java array indexes:

```text
0-based indexes
```

## 10. Common Mistakes

Avoid:

```text
1. Using this approach on unsorted array
2. Moving right when sum is too small
3. Moving left when sum is too big
4. Returning values instead of indexes
5. Forgetting LeetCode may expect 1-based indexes
6. Using HashMap unnecessarily when array is already sorted
```

## Practice

Implement:

```java
public static int[] twoSumSortedTwoPointers(int[] numbers, int target) {
    // your code
}
```

Test cases:

```java
twoSumSortedTwoPointers(new int[] {2, 7, 11, 15}, 9)    // [0, 1]
twoSumSortedTwoPointers(new int[] {1, 2, 3, 4, 6}, 6)   // [1, 3]
twoSumSortedTwoPointers(new int[] {1, 3, 4, 5, 7}, 12)  // [3, 4]
twoSumSortedTwoPointers(new int[] {1, 2, 3}, 10)        // []
```

Key takeaway:

```text
Sorted array + target pair = left/right two pointers.
```
