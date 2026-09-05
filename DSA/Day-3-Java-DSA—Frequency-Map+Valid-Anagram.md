Assuming you mean **Day 3 Java DSA**.

# Day 3 Java DSA — Frequency Map + Valid Anagram

## 1. Concept

Today’s problem:

```text
Valid Anagram
```

Two strings are anagrams if they contain the same characters with the same counts.

Example:

```java
s = "anagram"
t = "nagaram"
```

Output:

```java
true
```

Because both have:

```text
a → 3
n → 1
g → 1
r → 1
m → 1
```

Order does not matter. Count matters.

## 2. Feynman Explanation

Imagine two bags of letter tiles.

Bag 1:

```text
a n a g r a m
```

Bag 2:

```text
n a g a r a m
```

If both bags have the exact same letters with the exact same quantity, they are anagrams.

If one bag has extra or missing letters, not anagram.

## 3. 80/20 Rule

Remember this:

```text
When counts matter, use a frequency map.
```

For strings:

```text
character → count
```

Example:

```text
'a' → 3
'n' → 1
'g' → 1
```

## 4. First Check

Before counting, check length:

```java
if (s.length() != t.length()) {
    return false;
}
```

Why?

```text
If lengths are different, same character counts are impossible.
```

Example:

```text
"abc" and "ab" → false immediately
```

## 5. Brute Force / Sorting Approach

Sort both strings and compare.

```java
"anagram" → "aaagmnr"
"nagaram" → "aaagmnr"
```

If sorted strings are equal, anagram.

Time:

```text
O(n log n)
```

because sorting is used.

## 6. Optimized Approach

Use character count.

For lowercase English letters `a-z`, use:

```java
int[] count = new int[26];
```

Why 26?

```text
a to z = 26 letters
```

Logic:

```text
For every char in s → increase count
For every char in t → decrease count
At the end, all counts should be 0
```

## 7. Java Code

Create file:

```text
Day03ValidAnagram.java
```

Code:

```java
package dsa.practice;

import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

public class Day03ValidAnagram {

    public static void main(String[] args) {
        System.out.println(isAnagramUsingSorting("anagram", "nagaram")); // true
        System.out.println(isAnagramUsingSorting("rat", "car"));         // false

        System.out.println(isAnagramUsingHashMap("anagram", "nagaram")); // true
        System.out.println(isAnagramUsingHashMap("rat", "car"));         // false

        System.out.println(isAnagramOptimizedLowercase("anagram", "nagaram")); // true
        System.out.println(isAnagramOptimizedLowercase("rat", "car"));         // false
        System.out.println(isAnagramOptimizedLowercase("aacc", "ccac"));       // false
        System.out.println(isAnagramOptimizedLowercase("", ""));               // true
    }

    public static boolean isAnagramUsingSorting(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        char[] sChars = s.toCharArray();
        char[] tChars = t.toCharArray();

        Arrays.sort(sChars);
        Arrays.sort(tChars);

        return Arrays.equals(sChars, tChars);
    }

    public static boolean isAnagramUsingHashMap(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        Map<Character, Integer> countMap = new HashMap<>();

        for (char ch : s.toCharArray()) {
            countMap.put(ch, countMap.getOrDefault(ch, 0) + 1);
        }

        for (char ch : t.toCharArray()) {
            if (!countMap.containsKey(ch)) {
                return false;
            }

            countMap.put(ch, countMap.get(ch) - 1);

            if (countMap.get(ch) < 0) {
                return false;
            }
        }

        return true;
    }

    public static boolean isAnagramOptimizedLowercase(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        int[] count = new int[26];

        for (int i = 0; i < s.length(); i++) {
            count[s.charAt(i) - 'a']++;
            count[t.charAt(i) - 'a']--;
        }

        for (int value : count) {
            if (value != 0) {
                return false;
            }
        }

        return true;
    }
}
```

## 8. Dry Run

Input:

```java
s = "anagram"
t = "nagaram"
```

After counting `s`:

```text
a → 3
n → 1
g → 1
r → 1
m → 1
```

Then subtract characters from `t`.

If all counts become `0`, result is:

```java
true
```

For:

```java
s = "rat"
t = "car"
```

`c` appears in `t`, but not in `s`.

So result:

```java
false
```

## 9. Complexity

Sorting approach:

```text
Time: O(n log n)
Space: O(n)
```

HashMap approach:

```text
Time: O(n)
Space: O(k)
```

where `k` is number of unique characters.

Lowercase `a-z` array approach:

```text
Time: O(n)
Space: O(1)
```

because array size is always 26.

## 10. Interview Explanation

Say this:

```text
I first check length. Then I count character frequencies.
If both strings have the same character counts, they are anagrams.
For lowercase English letters, I can use int[26] for O(n) time and O(1) space.
For general characters, I would use HashMap<Character, Integer>.
```

## 11. Common Mistakes

Avoid:

```text
1. Checking only length
2. Checking only contains()
3. Ignoring duplicate character counts
4. Forgetting empty string case
5. Using int[26] when input can contain uppercase, spaces, or Unicode
```

Important:

```text
"aacc" and "ccac" are not anagrams
```

Because counts differ.

## Practice

Solve using `HashMap` first:

```java
public static boolean isAnagramUsingHashMap(String s, String t) {
    // your code
}
```

Then solve using `int[26]`:

```java
public static boolean isAnagramOptimizedLowercase(String s, String t) {
    // your code
}
```

Key takeaway:

```text
Anagram = same characters + same frequency.
Counts matter → frequency map.
```
