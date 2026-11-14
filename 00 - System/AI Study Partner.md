---
tags: [system]
---
# AI Study Partner

An AI assistant can be a great tutor, or a very fast way to skip the thinking that makes you learn. This note is about the first kind: an AI that gives **hints, not answers**.

> [!tip] Using Cursor?
> This repo includes a rule (`.cursor/rules/study-partner.mdc`) that makes Cursor's AI follow everything below automatically. With any other assistant, paste the [[#Rules for the AI]] block at the start of the chat.

## Starting a session
Tell it the problem, the pattern you're on, and where you are:
> "Today: **Group Anagrams** (Arrays & Hashing). Here's my attempt / I'm stuck at X."

## What a good AI partner does
- **Doesn't dump the solution.** It follows the hint ladder from [[Problem-Solving Method]]: a small nudge first, a bigger hint only when you ask.
- **Asks the questions you need to learn to ask yourself:** *"What's the brute force? What's repeated? What do the constraints allow?"*
- **Points to *where* a bug is** before saying *what* it is.
- **Writes the problem note** in the vault format after you solve it (frontmatter, Key Insight, code, review dates).
- **Ends with the Key Insight** in one sentence, plus the trigger that should have pointed to the pattern.

## Useful prompts
- "Give me hint 1 only."
- "Is my brute force right? What's the complexity?"
- "Which pattern is this, and which trigger should have told me?"
- "Quiz me on the Sliding Window pattern."
- "Give me 3 mixed problems from patterns I've finished, but don't tell me the pattern."
- "Review my week." (paste your weekly review)
- "Write the Obsidian note for this problem."

## Rules for the AI
Copy this into any AI chat before you start:

```text
You are my DSA study partner. I'm working through the NeetCode 150 by pattern, in Python.
- Never give the full solution or full code unless I say "show solution".
- Give hints one small step at a time: which pattern, then which trigger,
  then the key idea, then an outline in comments. Wait for me between steps.
- Before hinting, ask me: what's the brute force? what work is repeated?
  what do the constraints allow?
- If my code has a bug, tell me where to look before telling me what it is.
- Always end with the Key Insight in one sentence and the trigger that
  points to the pattern.
- When I ask for a problem note, set status to alone / hint / solution
  and next_review to +3 days if I solved it alone, +1 day otherwise.
```

## Rules for you
- Try for **25 minutes** (15 for an Easy) before asking for anything.
- Ask for **one hint at a time**, then go back to coding.
- If you needed hints, the problem is due again **tomorrow**. The re-solve is where the learning happens.
