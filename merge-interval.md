## PATTERN NAME: Merge Intervals

1) WHEN TO THINK OF THIS (Fast Pattern Recognition)
- If the problem mentions / implies overlapping ranges, intervals, meetings, schedules, timelines
- If input is a list of [start, end] pairs and output expects merged / condensed ranges
- If you need to detect conflicts, gaps, coverage, or union of ranges
- If sorting by start time simplifies reasoning
- If each element represents a continuous span on a number line
- NOT to use if intervals cannot be reordered or overlap definition is non-transitive

2) NAIVE APPROACH → WHY IT FAILS (Constraint Awareness)
- Compare every interval with every other and merge overlaps iteratively
- Re-scan list after each merge until stable
- Time complexity: O(n²)
- Fails for large n due to repeated overlap checks and cascading merges

3) KEY INSIGHT (Core Mental Model)
- After sorting by start, overlap decisions become local
- Only the “last merged interval” matters at any point
- Invariant: merged list is always non-overlapping and sorted
- Greedy dominance: once intervals are sorted, no future interval can overlap earlier than the last merged end

4) STANDARD SOLUTION TEMPLATE (State Transitions)
1. Sort intervals by start (primary), end (secondary)
2. Initialize result with first interval
3. Iterate remaining intervals
4. If current.start ≤ last.end → merge by extending last.end
5. Else → append current as new disjoint interval
6. Maintain invariant: result is sorted and non-overlapping

> Invariant:
- Result intervals are mutually exclusive and ordered by start

5) CANONICAL CODE SKELETON (Pseudocode)
```python
sort intervals by start

result = []
for interval in intervals:
    if result is empty:
        result.append(interval)
    else:
        last = result[-1]
        if interval.start <= last.end:
            last.end = max(last.end, interval.end)
        else:
            result.append(interval)

return result
```

> 6) DECISION CHECKLIST (Senior Clarifying Questions)
- Are interval boundaries inclusive or exclusive?
- Is input allowed to be mutated (sorting in-place)?
- Can intervals be extremely large (int overflow concerns)?
- Are intervals guaranteed valid (start ≤ end)?
- Is input already sorted?
- Can intervals arrive as a stream?

> 7) COMMON VARIATIONS & WHAT CHANGES
- Insert interval → binary search + local merge
- Count overlaps only → track active count instead of storing ranges
- Minimum meeting rooms → use heap instead of merge list
- Interval intersection → change merge condition to max(start), min(end)
- Gaps between intervals → emit gaps instead of merges
- Circular intervals → normalize or split before sorting

> 8) COMMON FAILURE PATTERNS (Why Candidates Fail)
- Forgetting to sort before merging
- Using < instead of ≤ for overlap checks
- Mutating wrong interval reference
- Breaking invariant by appending before merging
- Mishandling single-interval or empty input
- Overcomplicating with nested loops or stacks

> 9) TIME & SPACE COMPLEXITY (With Trade-offs)
- Time: O(n log n) due to sorting
- Space: O(n) for output, O(1) extra if in-place allowed
- Sorting is the unavoidable lower bound for unsorted input

> 10) SENIOR SIGNALS (Must Be Verbalized)
- Sorting converts global overlap problem into local decisions
- Greedy merge is optimal once sorted
- Invariant: result is always non-overlapping
- Pairwise comparison is unnecessary after sort
- Scaling concern: streaming requires different structure

> 11) PRACTICE PROBLEMS (Canonical Set)
- Merge Intervals
- Insert Interval
- Meeting Rooms
- Meeting Rooms II
- Interval List Intersections
- Non-overlapping Intervals
- Employee Free Time

> 12) INTERVIEW FOLLOW-UP QUESTIONS (Senior Level)
- What changes if intervals are streamed?
- How would you avoid sorting if input is partially ordered?
- How does this change with open vs closed intervals?
- Can this be parallelized?
- How would you handle billions of intervals?
- What breaks if intervals are circular?
- How would you store this in a database efficiently?