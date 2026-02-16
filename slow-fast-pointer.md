## PATTERN NAME: Fast and Slow Pointer (Tortoise–Hare)

> 1) WHEN TO THINK OF THIS (Fast Pattern Recognition)
- If the problem mentions / implies cycles, loops, repetition, or infinite traversal
- If traversal speed differences can reveal structure (cycle entry, midpoint)
- If working with linked lists, iterators, implicit graphs (array as next-index)
- If memory constraints forbid auxiliary data structures (no hash/set)
- If problem asks for cycle detection or middle element in one pass
- NOT suitable if random access or bidirectional traversal is required

> 2) NAIVE APPROACH → WHY IT FAILS (Constraint Awareness)
- Track visited nodes using hash set
- Traverse list twice to find length/middle
- Time: O(n), Space: O(n)
- Violates space constraints; unnecessary memory for deterministic structure

> 3) KEY INSIGHT (Core Mental Model)
- Two pointers moving at different speeds must meet in a cycle
- Relative speed converts spatial structure into temporal signal
- Invariant: distance gap changes deterministically per step
- Enables detection + localization without extra memory

> 4) STANDARD SOLUTION TEMPLATE (State Transitions)
1. Initialize slow = start, fast = start
2. Move slow by 1 step, fast by 2 steps
3. If fast reaches null → no cycle
4. If slow == fast → cycle detected
5. Reset one pointer to start (for entry problems)
6. Move both by 1 until they meet (cycle entry)

> Invariant:
- Fast gains exactly one step over slow per iteration inside cycle

> 5) CANONICAL CODE SKELETON (Pseudocode)
```python
slow = start
fast = start

while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
    if slow == fast:
        break

if not fast or not fast.next:
    return NO_CYCLE

slow = start
while slow != fast:
    slow = slow.next
    fast = fast.next

return MEETING_POINT
```

> 6) DECISION CHECKLIST (Senior Clarifying Questions)
- Is mutation of structure allowed?
- Can pointers reach null?
- Is cycle guaranteed or optional?
- Do we need detection only or entry point?
- Are nodes comparable by reference or value?
- Is structure singly or doubly linked?

> 7) COMMON VARIATIONS & WHAT CHANGES
- Find middle of list → stop when fast reaches end
- Detect cycle only → no reset phase
- Find cycle length → count steps after first meeting
- Happy number / array cycle → next = f(x)
- Duplicate number (array) → treat array as linked list

> 8) COMMON FAILURE PATTERNS (Why Candidates Fail)
- Not checking fast.next before advancing
- Incorrect reset logic for cycle entry
- Assuming value equality instead of reference
- Infinite loop due to wrong termination
- Applying pattern where traversal isn’t deterministic

> 9) TIME & SPACE COMPLEXITY (With Trade-offs)
- Time: O(n)
- Space: O(1)
- Dominates hash-based approach under memory constraints

> 10) SENIOR SIGNALS (Must Be Verbalized)
- Why speed differential guarantees meeting
- Why reset leads to cycle entry
- Why hash-set is inferior here
- Memory predictability in production systems

> 11) PRACTICE PROBLEMS (Canonical Set)
- Linked List Cycle
- Linked List Cycle II
- Find the Duplicate Number
- Happy Number
- Middle of the Linked List
- Circular Array Loop

> 12) INTERVIEW FOLLOW-UP QUESTIONS (Senior Level)
- Prove why pointers meet inside a cycle
- How do you compute cycle length?
- What changes if fast moves 3 steps?
- Can this be adapted to streams?
- Why does this work without extra memory?
- When would you prefer hashing instead?