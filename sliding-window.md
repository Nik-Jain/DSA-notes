## PATTERN NAME:Sliding Window

> 1) WHEN TO THINK OF THIS (Fast Pattern Recognition)
- If the problem involves contiguous subarrays or substrings
- If a range/window grows and shrinks dynamically
- If constraints involve max/min/sum/length/count/average/at most k/at least k/exactly k/longest/shortest within a subarray
- If brute force involves checking all subarrays
- NOT suitable if elements can be reordered or window condition is non-monotonic

> 2) NAIVE APPROACH → WHY IT FAILS (Constraint Awareness)
- Check all possible subarrays and validate condition
- Time complexity: O(n²) or worse
- Fails due to repeated recomputation of overlapping ranges

> 3) KEY INSIGHT (Core Mental Model)
- Window represents a valid contiguous state
- Amazon hire-fire example
- Expanding window explores possibilities
- Shrinking window restores invariant when condition breaks
- Each element enters and exits the window at most once

> 4) STANDARD SOLUTION TEMPLATE (State Transitions)
1. Decide if fixed or dynamic window needs be used
2. Identify which information will be required to check condition
3. Capture infomration and Check condition. If condition satisfies, update result.
3. Move/Expand/Shrink slide and repeate step 3.

> Invariant:
- Window always represents a valid or minimally invalid state

> 5) CANONICAL CODE SKELETON (Pseudocode)

##### Fixed Window
```python
low = 0; high = k -1
# Capture first window information
for each element in windiw:
    calculate information
# Capture all remaining window informations
while(high<n):
    update result
    slide window
    update information
```
##### Variable Window
```
low = 0; high = 0
for high in range of n:
    add high in information
    check if informat8ion is coreect or wrong
    check if information is correct or not
        if incorrect information, shrink or expand slide as per the need till the time information is not correct
    if infomrtaion correct, update result


```
> 6) DECISION CHECKLIST (Senior Clarifying Questions)
- Is the window condition monotonic?
- Are negative numbers present?
- Is exact match or at-most condition required?
- Can input be streamed?
- Is input modification allowed?

> 7) COMMON VARIATIONS & WHAT CHANGES
- Fixed-size window → no shrinking loop
- Longest valid window → update answer after shrink
- Count of subarrays → add (right - left + 1)
- String problems → frequency map instead of numeric state

> 8) COMMON FAILURE PATTERNS (Why Candidates Fail)
- Applying sliding window when condition is non-monotonic
- Forgetting to shrink window fully
- Incorrect invariant definition
- Misplacing answer update logic

> 9) TIME & SPACE COMPLEXITY (With Trade-offs)
- Time: O(n)
- Space: O(1) or O(k) depending on state
- Outperforms prefix sum for dynamic windows

> 10) SENIOR SIGNALS (Must Be Verbalized)
- Why sliding window is linear
- Why prefix sum fails here
- Invariant definition
- Streaming-friendly and cache-efficient

> 11) PRACTICE PROBLEMS (Canonical Set)
- Longest Substring Without Repeating Characters
- Minimum Size Subarray Sum
- Max Consecutive Ones III
- Permutation in String
- Longest Repeating Character Replacement

> 12) INTERVIEW FOLLOW-UP QUESTIONS (Senior Level)
- What breaks if negative numbers are introduced?
- How would this change for exact-sum conditions?
- Can this be parallelized?
- Why doesn’t prefix sum work here?
- How would you handle infinite streams?