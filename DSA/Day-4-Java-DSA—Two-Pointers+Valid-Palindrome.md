Assuming you mean **Day 4 Java DSA**.

# Day 4 Java DSA — Two Pointers + Valid Palindrome

## 1. Concept

Problem:

```text
Valid Palindrome
```

Check whether a string reads the same forward and backward.

Example:

```java
"madam" → true
"hello" → false
```

But real interview problem usually says:

```text
Ignore spaces, symbols, and case.
Only compare letters and digits.
```

Example:

```java
"A man, a plan, a canal: Panama"
```

After ignoring spaces/symbols/case:

```text
amanaplanacanalpanama
```

Output:

```java
true
```

## 2. Feynman Explanation

Imagine two people reading the same sentence.

One starts from the left side.

One starts from the right side.

They compare valid characters.

```text
If both characters match → move inward
If they do not match → not palindrome
```

If both people cross each other without mismatch:

```text
Palindrome
```

## 3. 80/20 Rule

Remember this:

```text
When comparing from both ends, use two pointers.
```

Use two pointers when you see:

```text
start and end comparison
palindrome
sorted pair checking
reverse-style comparison
```

## 4. Brute Force Approach

Clean the string first.

```java
"A man, a plan" → "amanaplan"
```

Then compare with reverse.

Problem:

```text
Extra string created
Space: O(n)
```

## 5. Optimized Approach

Use two pointers directly.

```java
left = 0
right = s.length() - 1
```

Rules:

```text
If left char is not letter/digit → left++
If right char is not letter/digit → right--
Compare lowercase left and right
If different → false
Else move inward
```

## 6. Java Code

Create file:

```text
Day04ValidPalindrome.java
```

Code:

```java
package dsa.practice;

public class Day04ValidPalindrome {

    public static void main(String[] args) {
        System.out.println(isPalindromeBruteForce("A man, a plan, a canal: Panama")); // true
        System.out.println(isPalindromeBruteForce("race a car"));                     // false

        System.out.println(isPalindromeTwoPointers("A man, a plan, a canal: Panama")); // true
        System.out.println(isPalindromeTwoPointers("race a car"));                     // false
        System.out.println(isPalindromeTwoPointers("madam"));                          // true
        System.out.println(isPalindromeTwoPointers(" "));                              // true
        System.out.println(isPalindromeTwoPointers("0P"));                             // false
        System.out.println(isPalindromeTwoPointers("No lemon, no melon"));             // true
    }

    public static boolean isPalindromeBruteForce(String s) {
        StringBuilder cleaned = new StringBuilder();

        for (char ch : s.toCharArray()) {
            if (Character.isLetterOrDigit(ch)) {
                cleaned.append(Character.toLowerCase(ch));
            }
        }

        String original = cleaned.toString();
        String reversed = cleaned.reverse().toString();

        return original.equals(reversed);
    }

    public static boolean isPalindromeTwoPointers(String s) {
        int left = 0;
        int right = s.length() - 1;

        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }

            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }

            char leftChar = Character.toLowerCase(s.charAt(left));
            char rightChar = Character.toLowerCase(s.charAt(right));

            if (leftChar != rightChar) {
                return false;
            }

            left++;
            right--;
        }

        return true;
    }
}
```

## 7. Dry Run

Input:

```java
"race a car"
```

Compare:

```text
r vs r → match
a vs a → match
c vs c → match
e vs a → mismatch
```

Output:

```java
false
```

Input:

```java
"A man, a plan, a canal: Panama"
```

We ignore:

```text
spaces
commas
colon
case difference
```

Valid comparison succeeds.

Output:

```java
true
```

## 8. Complexity

Brute force:

```text
Time: O(n)
Space: O(n)
```

Optimized two pointers:

```text
Time: O(n)
Space: O(1)
```

Why O(1) space?

```text
No extra cleaned string.
Only left, right, and a few variables.
```

## 9. Senior Java Notes

Use:

```java
Character.isLetterOrDigit(ch)
Character.toLowerCase(ch)
```

Avoid this in optimized solution:

```java
s.replaceAll(...)
```

Reason:

```text
Regex creates extra work and extra string.
```

For most DSA interviews, `charAt()` is enough. For full Unicode-heavy production text, you may need code-point handling, but for standard interview input this solution is accepted.

## 10. Common Mistakes

Avoid:

```text
1. Comparing without lowercasing
2. Not skipping symbols/spaces
3. Creating cleaned string in optimized solution
4. Moving only one pointer after match
5. Using left <= right unnecessarily
6. Returning false for empty string or only spaces
```

Important:

```java
" " → true
```

Because after ignoring spaces, empty string is considered palindrome.

## Practice

Implement only optimized method:

```java
public static boolean isPalindromeTwoPointers(String s) {
    // your code
}
```

Test cases:

```java
isPalindromeTwoPointers("A man, a plan, a canal: Panama") // true
isPalindromeTwoPointers("race a car")                     // false
isPalindromeTwoPointers("madam")                          // true
isPalindromeTwoPointers("")                               // true
isPalindromeTwoPointers("0P")                             // false
```

Key takeaway:

```text
Palindrome check = two pointers from both ends.
```
