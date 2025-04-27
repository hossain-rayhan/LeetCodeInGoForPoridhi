
# LeetCode 001: Two Sum

## Problem Statement

You are given:
- An array of integers called `nums`
- An integer called `target`

Your task is to **find two numbers** in the array such that **they add up to `target`**, and **return their indices**.

**Important rules:**
- Exactly one solution is guaranteed.
- Cannot use the same element twice.
- Return indices in any order.

## Example

```plaintext
Input: nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
Explanation: nums[0] + nums[1] = 2 + 7 = 9
```

## Solution 1: Memory Efficient but Slower

```go
func twoSum(nums []int, target int) []int {
    for i := 0; i < len(nums)-1; i++ {
        for j := i + 1; j < len(nums); j++ {
            if nums[i]+nums[j] == target {
                return []int{i, j}
            }
        }
    }
    return nil
}
```

### How it Works

- Use **two loops** to check every possible pair (`nums[i]` and `nums[j]`).
- If their sum is equal to `target`, return their indices immediately.
- If no solution is found (shouldn’t happen because one solution is guaranteed), return nil.

### Time and Space Complexity

- **Time:** O(N²) — because you have a nested loop.
- **Space:** O(1) — no extra memory used.

---


## Solution 2: Using a Map (Extra Memory) but Faster

```go
func twoSum(nums []int, target int) []int {
    indexMap := make(map[int]int)

    for i, num := range nums {
        if index, found := indexMap[target-num]; found {
            return []int{index, i}
        }
        indexMap[num] = i
    }

    return nil
}
```

### How it Works

Step-by-step:
1. **Create an empty map** called `indexMap` to store numbers and their indices as you go through the array.
2. **Loop over the array**:
   - For each `num`, check if `target - num` already exists in `indexMap`.
   - If it **does exist**, it means you found two numbers that add up to `target`!
   - **Return their indices** immediately.
3. If it doesn't exist:
   - Store the current `num` and its `index` in `indexMap`.
   - Keep going.
4. If no solution is found (shouldn’t happen because one solution is guaranteed), return `nil`.

### Time and Space Complexity

- **Time:** O(N) — You scan the list once.
- **Space:** O(N) — You store up to N numbers in the map.

