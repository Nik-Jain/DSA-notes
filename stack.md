## PATTERN NAME: Stack Pattern

> 1) WHEN TO THINK OF THIS (Fast Pattern Recognition)
- If the problem asks for **Next Greater/Smaller Element** to the left or right
- If the problem involves **nearest previous/next element satisfying a condition**
- If elements must be processed with **LIFO dependency**
- If the solution requires maintaining a **monotonic structure (increasing/decreasing)**
- If brute force requires **scanning left/right for every element**
- NOT suitable when relationships are **global rather than nearest-neighbor**

---

> 2) NAIVE APPROACH → WHY IT FAILS (Constraint Awareness)
- For each element, scan left/right to find next greater/smaller element
- Time complexity: **O(n²)**
- Repeated scanning of overlapping regions
- Becomes infeasible when **n ≥ 10⁵**

---

> 3) KEY INSIGHT (Core Mental Model)
- Maintain a **monotonic stack** storing unresolved elements
- Stack maintains an invariant: **ordered elements (increasing or decreasing)**
- When a new element violates the invariant → resolve stack elements
- Each element **pushed once and popped once → amortized O(n)**

---

> 4) STANDARD SOLUTION TEMPLATE (State Transitions)
1. Initialize an empty stack storing **indices or values**
2. Traverse the array sequentially
3. While stack not empty and **invariant violated**
4. Pop stack element and **resolve its answer**
5. Push current element to stack
6. After traversal, process any remaining stack elements

> Invariant:
- Stack maintains **monotonic ordering**

---

> 5) CANONICAL CODE SKELETON (Pseudocode)

```python
stack = []
result = initialize_result(n)

for i in range(n):

    while stack and violation_condition(arr[stack[-1]], arr[i]):
        idx = stack.pop()
        result[idx] = resolve(arr[i], idx)

    stack.append(i)

while stack:
    idx = stack.pop()
    result[idx] = default_value
```

> 6) DECISION CHECKLIST (Senior Clarifying Questions)
- Are we searching for next greater/smaller or previous greater/smaller?
- Should the stack store values or indices?
- How should duplicates be treated (strict vs non-strict comparisons)?
- Should traversal be left-to-right or right-to-left?
- Is the input size large enough to require O(n) solution?

> 7) COMMON VARIATIONS & WHAT CHANGES
- Next Greater Element → decreasing stack, resolve when larger element appears
- Next Smaller Element → increasing stack, resolve when smaller element appears
- Largest Rectangle in Histogram → stack stores increasing heights; compute area during pop
- Daily Temperatures → store indices and compute distance
- Stock Span Problem → collapse previous smaller values
- Remove K Digits → maintain monotonic stack to minimize number

> 8) COMMON FAILURE PATTERNS (Why Candidates Fail)
- Using stack when monotonic relationship does not exist
- Storing values instead of indices, losing position information
- Incorrect comparison operators with duplicates
- Forgetting post-processing of remaining stack elements
- Breaking invariant due to incorrect push/pop ordering
- Traversing in the wrong direction

> 9) TIME & SPACE COMPLEXITY (With Trade-offs)
- Time: O(n) amortized
- Space: O(n) worst case (strictly monotonic input)
- Brute force becomes impractical when n ≥ 10⁴

> 10) SENIOR SIGNALS (Must Be Verbalized)
- Brute force requires quadratic scanning
- Monotonic stack ensures each element processed at most twice
- Stack maintains order invariant enabling linear resolution
- Acceptable O(n) memory trade-off for significant time savings
- Efficient for single-pass processing and 
- streaming-style inputs

> 11) PRACTICE PROBLEMS (Canonical Set)
- Next Greater Element I
- Daily Temperatures
- Largest Rectangle in Histogram
- Trapping Rain Water
- Stock Span Problem
- Remove K Digits

> 12) INTERVIEW FOLLOW-UP QUESTIONS (Senior Level)
- How would you handle duplicate values differently?
- How can we compute both next greater and previous greater elements?
- How does the solution change for circular arrays?
- Can this be adapted for streaming input?
- How would the approach change for 2D matrices?
- When would a deque be more appropriate than a stack?
- Can space be optimized if only counts are required?