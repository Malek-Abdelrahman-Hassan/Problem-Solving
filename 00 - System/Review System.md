---
tags: [system]
---
# Review System (how you stop forgetting)

## The schedule

Every problem note has two properties: `next_review` and `review_count`.

| After | Review in |
|---|---|
| First solve (`hint` / `solution`) | **1 day** |
| First solve (`alone`) | **3 days** |
| Review 1 passed | 3 days |
| Review 2 passed | 7 days |
| Review 3 passed | 14 days |
| Review 4 passed | 30 days |
| Review 5 passed | **Done** (set `status: mastered`, remove `next_review`) |
| **Any review failed** | Back to **1 day**, `review_count: 0` |

The [[Dashboard]] shows everything due today.

## What a review is

A review is **not** re-reading your note or re-watching the video. It's:

1. Open the problem on LeetCode (or a blank file).
2. **Don't open your note yet.**
3. Say out loud: *"What's the pattern? What's the key insight?"*
4. Code it. **Timebox: 15 min** for a problem you've seen before.
5. Now open your note and compare.
   - Solved it cleanly: **pass**. Bump `review_count`, set the next date.
   - Needed to peek, or got stuck: **fail**. Reset to 1 day. Improve the Key Insight so it would have helped you.

> [!tip] Fast review mode
> On busy days you can do a **verbal review**: read the problem, then say (or write) the pattern, key insight, and complexity in under 2 minutes. It counts as a pass only if you're confident you could code it. Use this for problems at `review_count >= 3`.

## Pattern-level recall
Besides problems, review the **patterns themselves**:
- **Daily:** 5 min on [[Pattern Flashcards]] (triggers → pattern, pattern → template idea).
- **Weekly:** pick one finished pattern and type its template from memory. This is part of your weekly review (a new note in `05 - Weekly/` from the `Weekly Review` template).
- **Mixed days:** random problems from finished patterns, without knowing the pattern in advance.

## Optional plugin: Spaced Repetition
The community plugin **Spaced Repetition** (by st3v3nmw) can schedule the flashcards in [[Pattern Flashcards]] for you. Install it, open the flashcards note, and click "Review flashcards." It uses the `question::answer` format already in that note.
