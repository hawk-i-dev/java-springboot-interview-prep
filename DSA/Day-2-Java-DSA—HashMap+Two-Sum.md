Assuming you mean **Day 2 Java DSA**.

# Day 2 Java DSA — HashMap + Two Sum

## 1. Concept

Today’s problem:

```text
Two Sum
```

Given an integer array and a target, return indexes of two numbers whose sum equals target.

Example:

```java
nums = [2, 7, 11, 15]
target = 9
```

Output:

```java
[0, 1]
```

Because:

```text
nums[0] + nums[1] = 2 + 7 = 9
```

## 2. Feynman Explanation

Imagine you are shopping.

Target bill:

```text
₹9
```

You pick item `2`.

Now you ask:

```text
What do I need with 2 to make 9?
```

Answer:

```text
9 - 2 = 7
```

So for every number:

```text
needed = target - current number
```

If `needed` was already seen, answer found.

## 3. 80/20 Rule

Remember this:

```text
If you need fast lookup + index/value information, use HashMap.
```

Day 1:

```text
HashSet = only check existence
```

Day 2:

```text
HashMap = check existence + store index
```

## 4. Brute Force Approach

Check every pair.

```java
public static int[] twoSumBruteForce(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] == target) {
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

## 5. Optimized Approach Using HashMap

Store:

```text
number → index
```

Example:

```text
2 → 0
7 → 1
```

At each number:

```text
needed = target - num
```

If `needed` exists in map:

```text
return [seen.get(needed), currentIndex]
```

## 6. Java Code

Create file:

```text
Day02TwoSum.java
```

Code:

```java
package dsa.practice;

import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

public class Day02TwoSum {

    public static void main(String[] args) {
        System.out.println(Arrays.toString(twoSumBruteForce(new int[] {2, 7, 11, 15}, 9))); // [0, 1]
        System.out.println(Arrays.toString(twoSumBruteForce(new int[] {3, 2, 4}, 6)));      // [1, 2]

        System.out.println(Arrays.toString(twoSumUsingHashMap(new int[] {2, 7, 11, 15}, 9))); // [0, 1]
        System.out.println(Arrays.toString(twoSumUsingHashMap(new int[] {3, 2, 4}, 6)));      // [1, 2]
        System.out.println(Arrays.toString(twoSumUsingHashMap(new int[] {3, 3}, 6)));         // [0, 1]
        System.out.println(Arrays.toString(twoSumUsingHashMap(new int[] {1, 2, 3}, 10)));     // []
    }

    public static int[] twoSumBruteForce(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[] {i, j};
                }
            }
        }

        return new int[] {};
    }

    public static int[] twoSumUsingHashMap(int[] nums, int target) {
        Map<Integer, Integer> seen = new HashMap<>();

        for (int index = 0; index < nums.length; index++) {
            int current = nums[index];
            int needed = target - current;

            if (seen.containsKey(needed)) {
                return new int[] {seen.get(needed), index};
            }

            seen.put(current, index);
        }

        return new int[] {};
    }
}
```

Important Java point:

```java
Arrays.toString(result)
```

Use this to print arrays properly.

## 7. Dry Run

Input:

```java
nums = [2, 7, 11, 15]
target = 9
```

Steps:

```text
seen = {}

index = 0, current = 2
needed = 9 - 2 = 7
7 not found
save 2 → 0

seen = {2=0}

index = 1, current = 7
needed = 9 - 7 = 2
2 found in seen
return [0, 1]
```

## 8. Why Check Before Put?

For this case:

```java
nums = [3, 3]
target = 6
```

At index `0`:

```text
current = 3
needed = 3
seen empty
save 3 → 0
```

At index `1`:

```text
current = 3
needed = 3
seen has 3
return [0, 1]
```

If you save before checking, you may accidentally use the same index.

## 9. Complexity

Optimized solution:

```text
Time Complexity: O(n)
```

Because we loop once.

```text
Space Complexity: O(n)
```

Because HashMap may store many numbers.

## 10. Common Mistakes

Avoid:

```text
1. Returning values instead of indexes
2. Saving current number before checking needed
3. Using HashSet when index is required
4. Forgetting Arrays.toString() while printing int[]
5. Saying space is O(1) for HashMap solution
```

## Practice

Solve yourself:

```java
public static int[] twoSumUsingHashMap(int[] nums, int target) {
    // your code
}
```

Test cases:

```java
twoSumUsingHashMap(new int[] {2, 7, 11, 15}, 9)  // [0, 1]
twoSumUsingHashMap(new int[] {3, 2, 4}, 6)       // [1, 2]
twoSumUsingHashMap(new int[] {3, 3}, 6)          // [0, 1]
twoSumUsingHashMap(new int[] {-1, -2, -3}, -5)   // [1, 2]
```

Key takeaway:

```text
Two Sum on unsorted array = HashMap.
needed = target - current.
```
