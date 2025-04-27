# LeetCode 141: Linked List Cycle

## Problem Statement

Given `head`, the head of a singly linked list, determine if the linked list has a cycle in it. Return `true` if there is a cycle in the linked list; otherwise, return `false`.

## Go Solution

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func hasCycle(head *ListNode) bool {
    // If the list is empty or has only one node, there can't be a cycle
	if head == nil || head.Next == nil {
		return false
	}

	// Initialize two pointers: walker and runner
	walker := head
	runner := head

	// Traverse the list with the two pointers
	for runner != nil && runner.Next != nil {
		// Move the walker by one step and the runner by two steps
		walker = walker.Next
		runner = runner.Next.Next

		// If walker and runner meet, there is a cycle
		if walker == runner {
			return true
		}
	}

	// No cycle found
	return false
}
```

### How it Works

1. **Initialize two pointers**: We use two pointers, `walker` and `runner`, which both start at the head of the linked list. The `walker` pointer moves one step at a time, while the `runner` pointer moves two steps at a time.

2. **Traverse the list**: We iterate through the list until the `runner` pointer reaches the end (`nil`). In each iteration:
   - The `walker` pointer moves one step ahead.
   - The `runner` pointer moves two steps ahead.

3. **Cycle detection**: If at any point the `walker` and `runner` pointers meet (i.e., point to the same node), it indicates a cycle, and we return `true`.

4. **No cycle found**: If we reach the end of the list (`runner` or `runner.Next` is `nil`), it means there is no cycle, so we return `false`.

### Time and Space Complexity

- **Time Complexity**: O(N) — In the worst case, we traverse the list once, where `N` is the number of nodes in the linked list.
- **Space Complexity**: O(1) — We only use two pointers, so no extra space is required beyond the input.
