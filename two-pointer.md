## PATTERN NAME: Two Pointer

> 1) WHEN TO THINK OF THIS (Fast Pattern Recognition)
- Question has to be from array or linnked list
- If the problem mentions / implies sorted array, non-decreasing order, or can be sorted
- If the problem involves pairs, triplets, ranges, or comparisons between elements
- If question ask to remove duplicate/rarrange/merge in place
- If constraints ask for O(n) or O(n log n) where brute force is O(n²)
- If you need to shrink search space based on comparison results
- If pointers can move monotonically inward
- NOT suitable if pointer movement depends on non-monotonic conditions or random jumps

> 2) NAIVE APPROACH → WHY IT FAILS (Constraint Awareness)
- Check all pairs / subarrays using nested loops
- Time complexity: O(n²) or O(n³) (for triplets)
- Fails on large inputs due to quadratic explosion despite simple logic

> 3) KEY INSIGHT (Core Mental Model)
- Sorted order enables directional elimination
- Pointer movement preserves an ordering invariant
- Each pointer moves at most n times
- Dominates hash/brute force when ordering reduces search space deterministically

> Invariant:
- Left pointer only increases, right pointer only decreases
- All skipped states are provably invalid

> 4) STANDARD SOLUTION TEMPLATE (State Transitions)

- Ensure input is sorted (or justify sorting cost)
- Initialize pointers (l, r) at strategic boundaries
- Evaluate condition using l and r
- Move only one pointer based on comparison result
- Maintain invariant after each move
- Terminate when pointers cross

> 5) CANONICAL CODE SKELETON (Pseudocode)
```python
l = 0
r = n - 1

while l < r:
    state = evaluate(arr[l], arr[r])

    if state == VALID:
        update_result()
        move_pointer_based_on_goal()
    elif state == TOO_SMALL:
        l += 1      # preserve ordering invariant
    else:  # TOO_LARGE
        r -= 1      # preserve ordering invariant
```

> 6) DECISION CHECKLIST (Senior Clarifying Questions)
- Is the array already sorted, or is sorting allowed?
- Is input mutation acceptable?
- Are duplicates allowed and how should they be handled?
- Do we need all solutions or any one?
- Can pointers move only inward, or do we need resets?
- Is input size large enough to justify avoiding hashing?

> 7) COMMON VARIATIONS & WHAT CHANGES
- Opposite direction pointers → comparison logic
- Remove duplicates → skip equal neighbors
- Fixed-distance pointers → initialization only
- Triplet problems → outer loop + inner two pointers
- Partitioning problems → swap-based invariant
- String comparisons → character-based condition

> 8) COMMON FAILURE PATTERNS (Why Candidates Fail)
- Using two pointers without a sorted invariant
- Moving both pointers simultaneously without justification
- Incorrect duplicate skipping logic
- Missing termination conditions
- Updating result before invariant is valid
- Choosing two pointers when hashing is clearer

> 9) TIME & SPACE COMPLEXITY (With Trade-offs)
- Time: O(n) after sorting
- Sorting cost: O(n log n) if required
- Space: O(1) (in-place) or O(n) if copy/sort needed
- Trade-off vs hash set: lower memory, order-dependent

> 10) SENIOR SIGNALS (Must Be Verbalized)
- Why ordering enables deterministic pruning
- Why brute force explores dominated states
- Exact invariant being preserved
- Why pointer movement is monotonic
- Impact of sorting on total complexity
- Cache-friendly sequential access

> 11) PRACTICE PROBLEMS (Canonical Set)
- Two Sum II (Sorted Array)
- Container With Most Water
- 3Sum
- 4Sum
- Remove Duplicates from Sorted Array
- Valid Palindrome
- Trapping Rain Water

> 12) INTERVIEW FOLLOW-UP QUESTIONS (Senior Level)
- What changes if the array is not sorted?
- When would hashing outperform two pointers?
- How do you handle duplicate-heavy inputs?
- Can this work on a streaming input?
- How would you adapt this for k pointers?
- What breaks if comparison logic is non-monotonic?
- Is sorting still acceptable under tighter latency constraints?