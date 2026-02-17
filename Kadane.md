#### PATTERN NAME: Kadane Pattern (Maximum Subarray / Best Subarray Ending Here)

1) WHEN TO THINK OF THIS (Fast Pattern Recognition)
- If the problem mentions / implies maximum sum of a contiguous subarray
- If asked for best subarray ending at index i or local vs global optimum
- If brute force considers all subarrays and their sums
- If array contains positive and negative numbers
- If optimization depends on dropping a prefix when it hurts the sum
- NOT suitable if subarray must satisfy non-sum constraints (frequency, distinctness, exact length > 1 without aggregation)

2) NAIVE APPROACH → WHY IT FAILS (Constraint Awareness)
- Enumerate all subarrays and compute sum
- Time complexity: O(n²) (or O(n³) without prefix sums)
- Violates constraints for large n (10⁵+), redundant recomputation of overlapping sums

3) KEY INSIGHT (Core Mental Model)
- Optimal subarray ending at i either:
    - extends the optimal subarray ending at i−1, or
    - starts fresh at i
- Invariant: `current_best = max subarray sum ending exactly at index i`
- Negative prefix is always harmful → drop it
- Dominates divide-and-conquer due to single-pass, constant space

4) STANDARD SOLUTION TEMPLATE (State Transitions)
1. Initialize current_best to first element
2.  Initialize global_best to first element
3.  Iterate index i from 1 to n−1
4.  Decide: extend previous or restart at current
5.  Update current_best
6.  Update global_best

> Invariant
- current_best always represents max sum of subarray ending at current index

5) CANONICAL CODE SKELETON (Pseudocode)
```python
current_best = nums[0]
global_best = nums[0]

for i in range(1, n):
    current_best = max(nums[i], current_best + nums[i])
    global_best = max(global_best, current_best)

return global_best

```

> 6) DECISION CHECKLIST (Senior Clarifying Questions)
- Are all elements negative possible?
- Is empty subarray allowed or must pick at least one element?
- Do we need the subarray indices or only the sum?
- Is input streamable or stored entirely?
- Are there constraints on integer overflow?

> 7) COMMON VARIATIONS & WHAT CHANGES
- Return subarray indices → track start/reset positions
- Minimum subarray sum → invert comparison (min instead of max)
- Circular array max sum → Kadane + total sum − min subarray
- Max product subarray → track max and min states
- 2D max submatrix → compress rows + apply Kadane per column span

> 8) COMMON FAILURE PATTERNS (Why Candidates Fail)
- Resetting on < 0 without handling all-negative arrays
- Initializing current_best to 0 incorrectly
- Mixing global and local states
- Applying Kadane when problem is non-contiguous
- Forgetting index tracking when required

> 9) TIME & SPACE COMPLEXITY (With Trade-offs)
- Time: O(n) best / average / worst
- Space: O(1)
- Breakpoint: dominates divide-and-conquer (O(n log n)) for single query

> 10) SENIOR SIGNALS (Must Be Verbalized)
- Why greedy reset is correct (negative prefix invariant)
- Why divide-and-conquer is inferior here
- Definition of current_best invariant
- Streaming-friendly, cache-efficient, single pass

> 11) PRACTICE PROBLEMS (Canonical Set)
- Maximum Subarray
- Maximum Sum Circular Subarray
- Maximum Product Subarray
- Best Time to Buy and Sell Stock
- Maximum Submatrix Sum
- Flip Bits (binary string max ones)
- K-Concatenation Maximum Sum

> 12) INTERVIEW FOLLOW-UP QUESTIONS (Senior Level)
- How does this behave if all numbers are negative?
- How would you return the actual subarray?
- How does this extend to circular arrays?
- Why does greedy reset not miss the global optimum?
- Can this be adapted for streaming input?
- How does this change for product instead of sum?
- Can this be parallelized or segmented?
