==============================
PATTERN NAME:
Prefix and Suffix Sum

1) WHEN TO THINK OF THIS (Fast Pattern Recognition)
- If the problem mentions / implies range sum queries on static data
- If the problem mentions / implies sum/count of subarrays or substrings
- If the problem mentions / implies removing one element / splitting array / left-right contribution
- If the problem mentions / implies repeated overlapping range calculations
- If the problem mentions / implies “sum between i and j” with many queries
- NOT suitable if updates are frequent (then Fenwick/Segment Tree dominates)

2) NAIVE APPROACH → WHY IT FAILS (Constraint Awareness)
- For each range/subarray, compute sum by iterating elements
- Nested loops over start and end indices
- Time complexity: O(n²) or O(n³)
- Fails for n ≥ 10⁵ due to redundant recomputation

3) KEY INSIGHT (Core Mental Model)
- Precompute cumulative contribution once, reuse everywhere
- Prefix[i] stores aggregate from start → i (inclusive/exclusive)
- Range sum becomes constant-time subtraction
- Invariant: prefix[i] = prefix[i-1] + a[i]
- Dominates brute force when input is static and queries are many

4) STANDARD SOLUTION TEMPLATE (State Transitions)
1. Initialize prefix array of size n+1 with prefix[0] = 0
2. Build prefix cumulatively from left to right
3. (Optional) Build suffix cumulatively from right to left
4. Answer each query using prefix/suffix difference
5. Maintain invariant: prefix[k] = sum of a[0..k-1]

5) CANONICAL CODE SKELETON (Pseudocode)
```python
n = len(arr)
prefix = [0] * (n + 1)

for i in range(n):
    prefix[i + 1] = prefix[i] + arr[i]

# range sum [l, r] inclusive
range_sum = prefix[r + 1] - prefix[l]

# suffix (optional)
suffix = [0] * (n + 1)
for i in reversed(range(n)):
    suffix[i] = suffix[i + 1] + arr[i]
```

> 6) DECISION CHECKLIST (Senior Clarifying Questions)
- Are there updates after preprocessing?
- Are ranges inclusive or exclusive?
- Can negative numbers exist?
- How many queries vs input size?
- Is extra O(n) memory acceptable?
- Can input be streamed or must be stored?

> 7) COMMON VARIATIONS & WHAT CHANGES
- Range sum queries → simple prefix difference
- Count subarrays with sum = k → prefix + hashmap
- Product except self → prefix product + suffix product
- Left/right cost problems → prefix cost + suffix cost
- 2D matrix sum → 2D prefix sums
- Modulo constraints → apply mod at each accumulation

> 8) COMMON FAILURE PATTERNS (Why Candidates Fail)
- Off-by-one errors in prefix indexing
- Mixing inclusive/exclusive boundaries
- Forgetting prefix[0] = 0 invariant
- Using prefix sums when updates exist
- Overflow when values are large
- Incorrect handling of negative numbers in hashmap variant

> 9) TIME & SPACE COMPLEXITY (With Trade-offs)
-Preprocessing Time: O(n)
-Query Time: O(1)
-Space: O(n)
-Breakpoint: loses advantage if frequent point/range updates exist

> 10) SENIOR SIGNALS (Must Be Verbalized)
- Why preprocessing amortizes cost across queries
- Why sliding window fails for arbitrary range queries
- Prefix invariant definition
- Memory vs speed trade-off
- Suitability for static datasets and batch queries

> 11) PRACTICE PROBLEMS (Canonical Set)
- Range Sum Query – Immutable
- Subarray Sum Equals K
- Product of Array Except Self
- Find Pivot Index
- Corporate Flight Bookings
- Contiguous Array
- Maximum Size Subarray Sum Equals K

> 12) INTERVIEW FOLLOW-UP QUESTIONS (Senior Level)
- What changes if updates are introduced?
- How would you support millions of queries?
- How does this extend to 2D data?
- What breaks with integer overflow?
- How would you handle streaming input?
- Can this be parallelized?
- When would you reject this pattern outright?
