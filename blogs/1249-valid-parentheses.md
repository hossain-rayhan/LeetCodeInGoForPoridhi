# LeetCode 1249: Minimum Remove to Make Valid Parentheses

## Problem Statement

Given a string `s` consisting of `'('`, `')'`, and lowercase English characters, your task is to remove the minimum number of parentheses (either `'('` or `')'`, in any position) to make the resulting parentheses string valid.

A valid parentheses string is one where:
- It is empty.
- It only contains lowercase characters.
- It can be written as `AB` (where `A` and `B` are valid strings).
- It can be written as `(A)` (where `A` is a valid string).

### Example 1:
```plaintext
Input: s = "lee(t(c)o)de)"
Output: "lee(t(c)o)de"
Explanation: "lee(t(co)de)" , "lee(t(c)ode)" would also be accepted.
```

### Example 2:
```plaintext
Input: s = "a)b(c)d"
Output: "ab(c)d"
```

## Go Solution
```go
func minRemoveToMakeValid(s string) string {
    // Convert string to a slice of runes (characters)
    arr := []rune(s)
    leftParenthesesIndexStack := []int{}

    // Traverse through the string
    for i, char := range arr {
        if char == '(' {
            // Push index of '(' onto the stack
            leftParenthesesIndexStack = append(leftParenthesesIndexStack, i)
        } else if char == ')' {
            if len(leftParenthesesIndexStack) > 0 {
                // Pop from the stack if a matching '(' is found
                leftParenthesesIndexStack = leftParenthesesIndexStack[:len(leftParenthesesIndexStack)-1]
            } else {
                // Mark the unmatched ')' as invalid
                arr[i] = '*'
            }
        }
    }

    // Remove unmatched '(' by marking them as invalid
    for len(leftParenthesesIndexStack) > 0 {
        idx := leftParenthesesIndexStack[len(leftParenthesesIndexStack)-1]
        arr[idx] = '*'
        leftParenthesesIndexStack = leftParenthesesIndexStack[:len(leftParenthesesIndexStack)-1]
    }

    // Convert the modified slice back to a string, removing '*'
    result := string(arr)
    result = strings.ReplaceAll(result, "*", "")

    return result
}
```

### How it Works

1. **Traverse the string**: We go through each character in the string `s`.
    - When we encounter an `'('`, we push its index onto the stack.
    - When we encounter a `')'`, we check if there is a matching `'('` in the stack:
        - If yes, pop the stack (match the parentheses).
        - If no, mark the current `')'` as invalid (set it to `'*'`).

2. **Post-traversal cleanup**: After going through the string, any unmatched `'('` indices will still be in the stack. We go through the stack and mark these `'('` as invalid by setting them to `'*'`.

3. **Return the result**: Finally, we convert the modified slice back to a string, replacing all `'*'` with an empty string to remove the invalid characters.

### Time and Space Complexity

- **Time Complexity**: O(N) — We go through the string once, and each operation (push, pop, or mark) takes constant time.
- **Space Complexity**: O(N) — We use a stack to store indices, and in the worst case, we may store all indices.

