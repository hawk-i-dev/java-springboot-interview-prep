Assuming you mean **Day 1 Java DSA**.

# Day 1 Java DSA — Big-O + Array + HashSet

## 1. Concept

Today’s problem:

```text
Contains Duplicate
```

Given an integer array, return `true` if any number appears more than once.

Example:

```java
nums = [1, 2, 3, 1]
```

Output:

```java
true
```

Because `1` appears twice.

## 2. Feynman Explanation

Imagine you are checking IDs at an entry gate.

For every person:

```text
Have I already seen this ID?
```

If yes:

```text
Duplicate found
```

If no:

```text
Store this ID and continue
```

That storage is `HashSet`.

## 3. 80/20 Rule

Remember this:

```text
If you only need to check existence or duplicates, use HashSet.
```

Use:

```java
HashSet
```

when you need:

```text
Have I seen this value before?
Does this value already exist?
Are there duplicates?
```

## 4. Brute Force Approach

Compare every element with every other element.

```java
for i
    for j
        if nums[i] == nums[j]
```

Code:

```java
public static boolean containsDuplicateBruteForce(int[] nums) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[i] == nums[j]) {
                return true;
            }
        }
    }

    return false;
}
```

Complexity:

```text
Time: O(n²)
Space: O(1)
```

Problem: slow for large arrays.

## 5. Optimized Approach Using HashSet

Use a `HashSet` to remember numbers already seen.

```text
If number already exists in set → duplicate
Otherwise add it
```

## 6. Java Code

Create file:

```text
Day01ContainsDuplicate.java
```

Code:

```java
import java.util.HashSet;
import java.util.Set;

public class Day01ContainsDuplicate {

    public static boolean containsDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<>();

        for (int num : nums) {
            if (seen.contains(num)) {
                return true;
            }

            seen.add(num);
        }

        return false;
    }

    public static void main(String[] args) {
        System.out.println(containsDuplicate(new int[]{1, 2, 3, 1})); // true
        System.out.println(containsDuplicate(new int[]{1, 2, 3, 4})); // false
        System.out.println(containsDuplicate(new int[]{}));           // false
        System.out.println(containsDuplicate(new int[]{5}));          // false
        System.out.println(containsDuplicate(new int[]{10, 20, 10})); // true
    }
}
```

## 7. Senior Java Shortcut

`HashSet.add()` returns `false` if value already exists.

So this is cleaner:

```java
public static boolean containsDuplicate(int[] nums) {
    Set<Integer> seen = new HashSet<>();

    for (int num : nums) {
        if (!seen.add(num)) {
            return true;
        }
    }

    return false;
}
```

Meaning:

```text
Try to add num.
If add fails, num was already present.
So duplicate found.
```

## 8. Dry Run

Input:

```java
[1, 2, 3, 1]
```

Steps:

```text
seen = {}

num = 1
1 not in seen
seen = {1}

num = 2
2 not in seen
seen = {1, 2}

num = 3
3 not in seen
seen = {1, 2, 3}

num = 1
1 already in seen
return true
```

## 9. Complexity

```text
Time Complexity: O(n)
```

Because we loop once.

```text
Space Complexity: O(n)
```

Because in worst case all numbers are unique and stored in `HashSet`.

## 10. Java Interview Note

For `HashSet`, lookup is usually:

```text
O(1)
```

Because internally it uses hashing.

For custom objects, `HashSet` depends on:

```java
equals()
hashCode()
```

But for `Integer`, Java already handles it correctly.

## 11. Common Mistakes

Avoid:

```text
1. Using nested loops when HashSet is enough
2. Forgetting space complexity is O(n)
3. Saying HashSet keeps sorted order
4. Returning false too early inside loop
5. Confusing HashSet with HashMap
```

## 12. Practice

Solve this yourself:

```java
public static boolean containsDuplicate(int[] nums) {
    // your code
}
```

Test cases:

```java
containsDuplicate(new int[]{1, 2, 3, 1}) // true
containsDuplicate(new int[]{1, 2, 3, 4}) // false
containsDuplicate(new int[]{})           // false
containsDuplicate(new int[]{5})          // false
containsDuplicate(new int[]{-1, -2, -1}) // true
```

Key takeaway:

```text
Duplicate/existence check = HashSet.
```
