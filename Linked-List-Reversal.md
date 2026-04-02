PATTERN NAME:
Linked List Reversal

> 1) WHEN TO THINK OF THIS (Fast Pattern Recognition)
- If the problem mentions / implies reverse entire or part of a linked list
- If operations require reordering nodes without extra space
- If traversal requires changing direction of pointers
- If problem involves k-group reversal / pair swapping / palindrome check
- If constraints emphasize O(1) space and in-place modification
- NOT suitable if random access is required or array-based indexing is needed

> 2) NAIVE APPROACH → WHY IT FAILS (Constraint Awareness)
- Copy nodes into array → reverse → rebuild list
    - Time: O(n), Space: O(n)
- Stack-based reversal
    - Time: O(n), Space: O(n)
- Fails when in-place constraint or memory limits are strict

> 3) KEY INSIGHT (Core Mental Model)
- Reverse by re-pointing next pointers one by one
- Maintain invariant:
    - `prev` = reversed portion
    - `curr` = remaining list to process
- Each step extracts current node and prepends to reversed list
- Dominates alternatives due to O(1) space + single pass

> 4) STANDARD SOLUTION TEMPLATE (State Transitions)
1. Initialize: prev = None, curr = head
2. Iterate while curr exists
3. Store next node: next_node = curr.next
4. Reverse pointer: curr.next = prev
5. Move pointers:
    - `prev = curr`
    - `curr = next_node`
6. Return `prev` as new head
> Invariant:
- `prev` always points to correctly reversed prefix
- `curr` always points to unprocessed suffix
> 5) CANONICAL CODE SKELETON (Pseudocode)
```python
def reverse_list(head):
    prev = None
    curr = head
    
    while curr:
        next_node = curr.next      # preserve remainder
        curr.next = prev           # reverse link
        
        prev = curr                # move prev forward
        curr = next_node           # move curr forward
    
    return prev
```

> 6) DECISION CHECKLIST (Senior Clarifying Questions)
- Is in-place modification allowed?
- Do we reverse entire list or subpart (k-group / range)?
- What happens for empty / single node list?
- Are we allowed to change node values vs pointers?
- Is recursion acceptable given stack limits?
- Is input streaming or too large for recursion?

> 7) COMMON VARIATIONS & WHAT CHANGES
- Reverse Linked List II (range) → Maintain sublist boundaries + reconnect
- Reverse in K-Groups → Loop + check group size + partial reversal logic
- Swap Nodes in Pairs → Reverse fixed size = 2
- Reverse for Palindrome Check → Reverse second half only
- Reverse Doubly Linked List → Swap next and prev pointers
- Recursive Reversal → Same invariant, but handled via call stack

> 8) COMMON FAILURE PATTERNS (Why Candidates Fail)
- Losing reference to remaining list (next_node not stored)
- Incorrect pointer update order (breaks list)
- Returning wrong head (should return prev)
- Infinite loop due to pointer mismanagement
- Mishandling edge cases (null / single node)
- Mixing node value swap vs pointer reversal

> 9) TIME & SPACE COMPLEXITY (With Trade-offs)
- Time: O(n) (Best / Avg / Worst)
- Space:
    - Iterative: O(1)
    - Recursive: O(n) (call stack)
- Trade-off: recursion cleaner but stack overflow risk for large n

> 10) SENIOR SIGNALS (Must Be Verbalized)
- Optimal due to single pass + constant space
- Array/stack approaches fail space constraints
- Core invariant: prev = reversed, curr = remaining
- Safe pointer manipulation requires strict ordering
- Production concern: avoid recursion for large lists

> 11) PRACTICE PROBLEMS (Canonical Set)
- Reverse Linked List
- Reverse Linked List II
- Reverse Nodes in k-Group
- Swap Nodes in Pairs
- Palindrome Linked List
- Reorder List

> 12) INTERVIEW FOLLOW-UP QUESTIONS (Senior Level)
- How would you reverse only k nodes if remaining < k?
- Can this be done recursively and iteratively—trade-offs?
- How do you handle very large lists (millions of nodes)?
- What changes for doubly linked list?
- Can reversal be done in a streaming scenario?
- How would you detect and reverse cycle portion?
- How to make this thread-safe / concurrent-safe?
