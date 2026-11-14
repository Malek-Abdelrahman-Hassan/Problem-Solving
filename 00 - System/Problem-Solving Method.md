---
tags: [system]
---
# Problem-Solving Method

Use this **every time** you open a problem. It gives you something concrete to do, so you're never stuck at a blank screen.

---

## Step 1: Understand (3–5 min)
- Restate the problem in **one sentence** in your own words.
- Write down **input, output, constraints**. The constraints tell you the target complexity (see [[Pattern Recognition Cheatsheet#Constraints tell you the complexity]]).
- Work **one example by hand**, then make up one **edge case** (empty, single element, all same, negatives, duplicates).

## Step 2: Brute force first (3–5 min)
- What's the dumbest correct solution? Usually nested loops or "try everything."
- Say its complexity out loud. **You don't have to code it.** You need it because the optimal solution is usually "brute force minus the repeated work."

> [!tip] The question that finds the optimization
> "What work is my brute force **repeating**?" Then: "Which data structure or pattern removes that repetition?"
> - Repeated lookups → **hash map**
> - Re-scanning a range → **sliding window / prefix sum**
> - Searching a sorted space → **binary search**
> - Recomputing the same subproblem → **DP / memoization**
> - Repeatedly finding the min/max → **heap**

## Step 3: Match the pattern (2–5 min)
- Scan for **triggers** using the [[Pattern Recognition Cheatsheet]].
- Pick a pattern and open its note. Look at the **template**.
- Ask: "What's my window / my pointers / my state / my graph here?"

## Step 4: Plan in comments (5 min)
Write the algorithm as **comments** before any code:
```python
# sort the array
# for each i: fix nums[i], two pointers on the rest
#   skip duplicates for i
#   if sum < 0 move left, > 0 move right, == 0 record and skip dupes
```
If you can't write the comments, you don't have a plan yet. Go back to Step 3.

## Step 5: Code (15 min)
Turn each comment into code. Keep the template's shape.

## Step 6: Test (5 min)
- Walk through your example **line by line** (be the computer).
- Run the edge cases.
- State the final **time and space** complexity.

---

## The 25-minute rule + hint ladder

If you're stuck **25 minutes** in (15 for an Easy), go down this ladder **one step at a time**, and try again after each step:

1. **Re-read the pattern note** for the pattern you think it is.
2. **Check the triggers again.** Is it a different pattern?
3. **NeetCode hint / topic tag** on LeetCode.
4. **Watch only the first part of the video**, the explanation, until the key idea appears. **Stop the video.** Code it yourself.
5. **Full video.** Then **close it** and code the solution from memory in a blank file.

Then in the problem note:
- `status: alone` = solved with no help
- `status: hint` = needed steps 1–4
- `status: solution` = needed step 5

> [!important] The non-negotiable rule
> If status is `hint` or `solution`, set `next_review` to **tomorrow** and re-solve it from scratch then. Most of the learning happens in that re-solve, not in the video.

## After solving: the Key Insight
Before closing the problem, write **one sentence** that would let future-you solve it again. Not the code, the trick.

Good: *"Sort, fix one number, then it's Two Sum II on the rest with two pointers; skip duplicates."*
Bad: *"Used two pointers."*
