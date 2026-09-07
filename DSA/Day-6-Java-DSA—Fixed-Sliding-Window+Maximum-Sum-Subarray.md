Assuming you mean **Day 6 Java DSA**.

# Day 6 Java DSA — Fixed Sliding Window + Maximum Sum Subarray

## 1. Concept

Problem:

```text
Find the maximum sum of any continuous subarray of size k.
```

Example:

```java
nums = [2, 1, 5, 1, 3, 2]
k = 3
```

Possible windows:

```text
2 + 1 + 5 = 8
1 + 5 + 1 = 7
5 + 1 + 3 = 9
1 + 3 + 2 = 6
```

Answer:

```text
9
```

## 2. Feynman Explanation

Imagine a window covering exactly `k` numbers.

When the window moves right:

```text
Remove the left number
Add the new right number
```

No need to calculate the full sum again.

## 3. 80/20 Rule

Remember:

```text
Fixed-size continuous subarray problem → Sliding Window
```

Keywords:

```text
subarray
continuous
consecutive
size k
maximum/minimum sum
```

## 4. Brute Force Approach

For every index, calculate the next `k` numbers.

```java
public static int maxSumSubarrayBruteForce(int[] nums, int k) {
    if (k <= 0 || k > nums.length) {
        throw new IllegalArgumentException("Invalid k");
    }

    int maxSum = Integer.MIN_VALUE;

    for (int i = 0; i <= nums.length - k; i++) {
        int currentSum = 0;

        for (int j = i; j < i + k; j++) {
            currentSum += nums[j];
        }

        maxSum = Math.max(maxSum, currentSum);
    }

    return maxSum;
}
```

Complexity:

```text
Time: O(n * k)
Space: O(1)
```

## 5. Optimized Sliding Window

Steps:

```text
1. Calculate sum of first k numbers
2. Store it as maxSum
3. Slide window one step
4. Subtract outgoing left value
5. Add incoming right value
6. Update maxSum
```

## 6. Java Code

Create:

```text
Day06MaxSumSubarray.java
```

Code:

```java
package dsa.practice;

public class Day06MaxSumSubarray {

    public static void main(String[] args) {
        System.out.println(maxSumSubarrayBruteForce(new int[] {2, 1, 5, 1, 3, 2}, 3)); // 9

        System.out.println(maxSumSubarraySlidingWindow(new int[] {2, 1, 5, 1, 3, 2}, 3)); // 9
        System.out.println(maxSumSubarraySlidingWindow(new int[] {1, 2, 3, 4, 5}, 2));    // 9
        System.out.println(maxSumSubarraySlidingWindow(new int[] {5, 1, 2}, 1));          // 5
        System.out.println(maxSumSubarraySlidingWindow(new int[] {-2, -1, -5}, 2));       // -3
    }

    public static int maxSumSubarrayBruteForce(int[] nums, int k) {
        if (k <= 0 || k > nums.length) {
            throw new IllegalArgumentException("Invalid k");
        }

        int maxSum = Integer.MIN_VALUE;

        for (int i = 0; i <= nums.length - k; i++) {
            int currentSum = 0;

            for (int j = i; j < i + k; j++) {
                currentSum += nums[j];
            }

            maxSum = Math.max(maxSum, currentSum);
        }

        return maxSum;
    }

    public static int maxSumSubarraySlidingWindow(int[] nums, int k) {
        if (k <= 0 || k > nums.length) {
            throw new IllegalArgumentException("Invalid k");
        }

        int windowSum = 0;

        for (int i = 0; i < k; i++) {
            windowSum += nums[i];
        }

        int maxSum = windowSum;

        for (int right = k; right < nums.length; right++) {
            int outgoing = nums[right - k];
            int incoming = nums[right];

            windowSum = windowSum - outgoing + incoming;
            maxSum = Math.max(maxSum, windowSum);
        }

        return maxSum;
    }
}
```

## 7. Dry Run

Input:

```java
nums = [2, 1, 5, 1, 3, 2]
k = 3
```

First window:

```text
2 + 1 + 5 = 8
maxSum = 8
```

Slide 1:

```text
Remove 2, add 1
windowSum = 8 - 2 + 1 = 7
maxSum = 8
```

Slide 2:

```text
Remove 1, add 3
windowSum = 7 - 1 + 3 = 9
maxSum = 9
```

Slide 3:

```text
Remove 5, add 2
windowSum = 9 - 5 + 2 = 6
maxSum = 9
```

Answer:

```text
9
```

## 8. Complexity

Optimized solution:

```text
Time: O(n)
Space: O(1)
```

Reason:

```text
Each element enters/leaves the window once.
```

## 9. Common Mistakes

Avoid:

```text
1. Recalculating every window fully
2. Using nested loops in optimized solution
3. Forgetting to subtract outgoing value
4. Forgetting to add incoming value
5. Initializing maxSum = 0 when array may contain negatives
6. Not validating k
```

Important:

```java
int maxSum = 0;
```

is wrong for:

```java
[-2, -1, -5]
```

Correct:

```java
int maxSum = windowSum;
```

## 10. Interview Explanation

Say:

```text
Since the window size is fixed, I calculate the first window sum once.
Then for every next window, I subtract the element leaving the window and add the new element entering the window.
This avoids repeated work and reduces time from O(n * k) to O(n).
```

Key takeaway:

```text
Fixed-size window = subtract outgoing + add incoming.
```
