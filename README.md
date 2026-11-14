# DSA Patterns: the NeetCode 150, Learned by Pattern

A free, open study system for data structures and algorithms interviews, in Python.

You don't need to memorize 150 solutions. You need about **18 patterns**, the **signals** that tell you which pattern a new problem wants, and a **review schedule** so you don't forget them. This repo gives you all three, organized around the [NeetCode 150](https://neetcode.io/practice) problem list.

It's built as an [Obsidian](https://obsidian.md) vault, but every note is plain Markdown, so you can read all of it right here on GitHub.

## Who this is for

- You can follow a solution video, but you get stuck when you open a **new** problem on your own.
- You solve problems, and a few weeks later you **can't solve them again**.
- You've started a problem list before and **didn't finish it**.

Each of these has a different cause and a different fix. [Why You Forget (and the Fix)](<00 - System/Why You Forget (and the Fix).md>) explains all three.

## The approach

1. **Patterns, not problems.** Each pattern note has the trigger words that point to it, the core idea, Python templates, tricks, common mistakes, and its NeetCode 150 checklist.
2. **A method for a blank screen.** The [Problem-Solving Method](<00 - System/Problem-Solving Method.md>) gives you fixed steps (understand → brute force → match the pattern → plan in comments → code → test), plus a hint ladder for when you're stuck.
3. **Spaced repetition.** Re-solve each problem after 1, 3, 7, 14 and 30 days. The [Review System](<00 - System/Review System.md>) explains how, and the Dashboard shows what's due today.
4. **A plan you can finish.** A [Study Plan](<00 - System/Study Plan.md>) in three phases, and [Commitment Rules](<00 - System/Commitment Rules.md>) built on habits instead of motivation ("minimum day," "never miss twice").

## The 18 patterns

| # | Pattern | Problems | Phase |
|---|---|---|---|
| 1 | [Arrays & Hashing](<01 - Patterns/Arrays & Hashing.md>) | 9 | 1: Foundations |
| 2 | [Two Pointers](<01 - Patterns/Two Pointers.md>) | 5 | 1: Foundations |
| 3 | [Sliding Window](<01 - Patterns/Sliding Window.md>) | 6 | 1: Foundations |
| 4 | [Stack](<01 - Patterns/Stack.md>) | 7 | 1: Foundations |
| 5 | [Binary Search](<01 - Patterns/Binary Search.md>) | 7 | 1: Foundations |
| 6 | [Linked List](<01 - Patterns/Linked List.md>) | 11 | 1: Foundations |
| 7 | [Trees](<01 - Patterns/Trees.md>) | 15 | 2: Recursion & Structures |
| 8 | [Tries](<01 - Patterns/Tries.md>) | 3 | 2: Recursion & Structures |
| 9 | [Heap / Priority Queue](<01 - Patterns/Heap - Priority Queue.md>) | 7 | 2: Recursion & Structures |
| 10 | [Backtracking](<01 - Patterns/Backtracking.md>) | 9 | 2: Recursion & Structures |
| 11 | [Graphs](<01 - Patterns/Graphs.md>) | 13 | 2: Recursion & Structures |
| 12 | [1-D Dynamic Programming](<01 - Patterns/1-D Dynamic Programming.md>) | 12 | 3: Optimization |
| 13 | [2-D Dynamic Programming](<01 - Patterns/2-D Dynamic Programming.md>) | 11 | 3: Optimization |
| 14 | [Greedy](<01 - Patterns/Greedy.md>) | 8 | 3: Optimization |
| 15 | [Intervals](<01 - Patterns/Intervals.md>) | 6 | 3: Optimization |
| 16 | [Advanced Graphs](<01 - Patterns/Advanced Graphs.md>) | 6 | 3: Optimization |
| 17 | [Math & Geometry](<01 - Patterns/Math & Geometry.md>) | 8 | 3: Optimization |
| 18 | [Bit Manipulation](<01 - Patterns/Bit Manipulation.md>) | 7 | 3: Optimization |
| | **Total** | **150** | |

## Quick references

- [Pattern Recognition Cheatsheet](<01 - Patterns/Pattern Recognition Cheatsheet.md>): "I see X in the problem, so I try Y," what the constraints tell you about the target complexity, and Python Big-O costs.
- [Pattern Flashcards](<03 - Flashcards/Pattern Flashcards.md>): trigger → pattern cards for 5 minutes of daily recall.
- [Example problem note](<00 - System/Example - Two Sum.md>): what a finished note looks like (Key Insight, triggers, brute force, optimal approach, review log).

## Use it for your own practice

### 1. Get your own copy
Fork this repo, or download it (green **Code** button → **Download ZIP**).

> [!TIP]
> Your personal notes stay private by default. `.gitignore` keeps `02 - Problems/`, `04 - Daily/` and `05 - Weekly/` out of git, so you can push your copy publicly without sharing your progress. Those notes then exist only on your machine, so back them up another way (Obsidian Sync, OneDrive, Dropbox, or a separate private repo).

### 2. Open it in Obsidian
1. Install Obsidian, then **Open folder as vault** and pick this folder.
2. Settings → Community plugins → turn off Restricted mode → Browse and install:
   - **Dataview** (required for `Dashboard.md`)
   - **Spaced Repetition** (optional, schedules the flashcards)
3. Open `Home.md` and read the "Start here" notes in order.

The vault is already configured so that:
- Clicking a problem link in a pattern note (e.g. `[[Group Anagrams]]`) creates the note in `02 - Problems/`.
- **Insert template** (core Templates plugin) uses the `Templates/` folder. Insert `Problem` into each new problem note.
- **Open today's daily note** creates it in `04 - Daily/` from the `Daily Log` template.

> [!WARNING]
> Don't type into the files in `Templates/`. They're blueprints: create a new note, then use **Insert template**.

### 3. The daily loop (60–90 min)
1. Open `Dashboard.md` and re-solve the problems due today.
2. Solve 1 new problem from the pattern you're on, following the [Problem-Solving Method](<00 - System/Problem-Solving Method.md>).
3. Create its note from the `Problem` template. Write the **Key Insight** and set `next_review`.
4. Spend 5 minutes on flashcards.

**Once a week:** create a note in `05 - Weekly/` (e.g. `2026-W40`) and insert the `Weekly Review` template.

**On a bad day:** 1 review + 15 minutes still counts. Just don't miss two days in a row.

## Study with an AI (optional)

An AI assistant is great for hints and terrible if it hands you the answer. [AI Study Partner](<00 - System/AI Study Partner.md>) has a copy-paste rule block for any chat assistant. If you use [Cursor](https://cursor.com), the included rule in `.cursor/rules/` applies it automatically: hints one step at a time, no full code unless you say "show solution," and problem notes written in the vault format with the right review date.

## Folder structure

| Path | Contents |
|---|---|
| `Home.md` | Entry point, with links to everything |
| `Dashboard.md` | Reviews due today, upcoming reviews, progress per pattern (needs Dataview) |
| `00 - System/` | Why you forget, study plan, problem-solving method, review system, commitment rules, AI study partner, example problem note |
| `01 - Patterns/` | 18 pattern notes + the pattern recognition cheatsheet |
| `02 - Problems/` | Your notes, one per solved problem (git-ignored) |
| `03 - Flashcards/` | Flashcards in `question::answer` format |
| `04 - Daily/` | Your daily logs (git-ignored) |
| `05 - Weekly/` | Your weekly reviews (git-ignored) |
| `Templates/` | Problem, Daily Log and Weekly Review templates |

## Contributing

Found a bug in a template, a clearer trigger, or a trick that's missing? Issues and pull requests are welcome. Please keep the existing style: Python, short templates that are easy to type from memory, and one idea per bullet.

## Credits

The problem list and roadmap order come from [NeetCode](https://neetcode.io); the problems themselves are on [LeetCode](https://leetcode.com). This project isn't affiliated with either. It's a study companion for working through their list.
