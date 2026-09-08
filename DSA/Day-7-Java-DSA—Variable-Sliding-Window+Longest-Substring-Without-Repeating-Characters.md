Assuming you mean **Day 7 Java DSA**.

# Day 7 Java DSA — Variable Sliding Window + Longest Substring Without Repeating Characters

## 1. Concept

Problem:

```text
Find the length of the longest substring without repeating characters.
```

Example:

```java
s = "abcabcbb"
```

Output:

```text
3
```

Because longest valid substrings are:

```text
abc
bca
cab
```

Length is:

```text
3
```

## 2. Feynman Explanation

Imagine a rubber band around characters.

You keep expanding the right side.

```text
a
ab
abc
```

When duplicate comes:

```text
abca
```

Now window is invalid because `a` repeated.

So shrink from left until duplicate is removed.

```text
bca
```

That is variable sliding window.

## 3. 80/20 Rule

Remember:

```text
Expand right. If window becomes invalid, move left until valid again.
```

For this problem:

```text
Valid window = no duplicate characters
```

## 4. Brute Force Idea

Try every substring and check if it has duplicates.

Complexity:

```text
Time: O(n²) or worse
Space: O(k)
```

Not good for large strings.

## 5. Optimized Approach Using HashSet

Use:

```java
Set<Character> seen = new HashSet<>();
```

Meaning:

```text
seen contains characters currently inside the window.
```

Rules:

```text
1. Move right character by character
2. If duplicate found, remove from left
3. Continue until window becomes valid
4. Add current character
5. Update max length
```

## 6. Java Code — HashSet Sliding Window

Create file:

```text
Day07LongestSubstring.java
```

Code:

```java
package dsa.practice;

import java.util.HashSet;
import java.util.Set;

public class Day07LongestSubstring {

    public static void main(String[] args) {
        System.out.println(lengthOfLongestSubstringUsingSet("abcabcbb")); // 3
        System.out.println(lengthOfLongestSubstringUsingSet("bbbbb"));    // 1
        System.out.println(lengthOfLongestSubstringUsingSet("pwwkew"));   // 3
        System.out.println(lengthOfLongestSubstringUsingSet("dvdf"));     // 3
        System.out.println(lengthOfLongestSubstringUsingSet("abba"));     // 2
        System.out.println(lengthOfLongestSubstringUsingSet(""));         // 0
    }

    public static int lengthOfLongestSubstringUsingSet(String s) {
        if (s == null || s.isEmpty()) {
            return 0;
        }

        Set<Character> seen = new HashSet<>();

        int left = 0;
        int maxLength = 0;

        for (int right = 0; right < s.length(); right++) {
            char currentChar = s.charAt(right);

            while (seen.contains(currentChar)) {
                seen.remove(s.charAt(left));
                left++;
            }

            seen.add(currentChar);

            int currentLength = right - left + 1;
            maxLength = Math.max(maxLength, currentLength);
        }

        return maxLength;
    }
}
```

## 7. Dry Run

Input:

```java
s = "abcabcbb"
```

Steps:

```text
a       → valid, max = 1
ab      → valid, max = 2
abc     → valid, max = 3
abca    → duplicate a
remove a from left
bca     → valid, max = 3
bcab    → duplicate b
remove b from left
cab     → valid, max = 3
```

Final answer:

```text
3
```

## 8. Better Java Interview Version — HashMap

This version jumps `left` directly instead of removing one by one.

Use:

```text
character → last seen index
```

```java
package dsa.practice;

import java.util.HashMap;
import java.util.Map;

public class Day07LongestSubstringOptimized {

    public static void main(String[] args) {
        System.out.println(lengthOfLongestSubstringUsingMap("abcabcbb")); // 3
        System.out.println(lengthOfLongestSubstringUsingMap("bbbbb"));    // 1
        System.out.println(lengthOfLongestSubstringUsingMap("pwwkew"));   // 3
        System.out.println(lengthOfLongestSubstringUsingMap("abba"));     // 2
    }

    public static int lengthOfLongestSubstringUsingMap(String s) {
        if (s == null || s.isEmpty()) {
            return 0;
        }

        Map<Character, Integer> lastSeen = new HashMap<>();

        int left = 0;
        int maxLength = 0;

        for (int right = 0; right < s.length(); right++) {
            char currentChar = s.charAt(right);

            if (lastSeen.containsKey(currentChar) && lastSeen.get(currentChar) >= left) {
                left = lastSeen.get(currentChar) + 1;
            }

            lastSeen.put(currentChar, right);

            int currentLength = right - left + 1;
            maxLength = Math.max(maxLength, currentLength);
        }

        return maxLength;
    }
}
```

## 9. Why `lastSeen.get(currentChar) >= left`?

Example:

```java
s = "abba"
```

When we reach second `a`, old `a` is already outside the current window.

So do not move `left` backward.

This check prevents wrong answers.

## 10. Complexity

HashSet version:

```text
Time: O(n)
Space: O(k)
```

HashMap version:

```text
Time: O(n)
Space: O(k)
```

Where:

```text
k = number of unique characters
```

## 11. Common Mistakes

Avoid:

```text
1. Confusing substring with subsequence
2. Updating max before removing duplicate
3. Moving left only once when using HashSet
4. Moving left backward in HashMap version
5. Forgetting empty string case
```

## 12. Interview Explanation

Say:

```text
I use variable sliding window.
The window is valid when it has no duplicate characters.
I expand right one character at a time.
If duplicate appears, I move left until the duplicate is removed.
Then I update max length.
This gives O(n) time because each character is processed at most twice.
```

Key takeaway:

```text
Longest valid substring = variable sliding window.
Invalid window? Shrink from left.
```
