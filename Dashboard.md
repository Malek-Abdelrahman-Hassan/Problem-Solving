---
tags: [home]
---
# Dashboard

> [!info] Requires the **Dataview** community plugin
> Settings → Community plugins → Browse → "Dataview" → Install → Enable. Without it, the blocks below show as code.

## Due for review today
```dataview
TABLE WITHOUT ID
  file.link AS Problem,
  pattern AS Pattern,
  difficulty AS Difficulty,
  status AS "Last result",
  review_count AS Reviews,
  next_review AS Due
FROM "02 - Problems" and #problem
WHERE next_review AND next_review <= date(today)
SORT next_review ASC
```

## Coming up this week
```dataview
TABLE WITHOUT ID
  file.link AS Problem,
  pattern AS Pattern,
  next_review AS Due
FROM "02 - Problems" and #problem
WHERE next_review AND next_review > date(today) AND next_review <= date(today) + dur(7 days)
SORT next_review ASC
```

## Progress by pattern
```dataview
TABLE WITHOUT ID
  key AS Pattern,
  length(rows) AS Solved,
  length(filter(rows.status, (s) => s = "alone" OR s = "mastered")) AS "Alone / Mastered"
FROM "02 - Problems" and #problem
GROUP BY pattern
SORT length(rows) DESC
```

## Needed the full solution (re-solve these first)
```dataview
LIST pattern
FROM "02 - Problems" and #problem
WHERE status = "solution"
SORT date_solved DESC
```

## Recently solved
```dataview
TABLE WITHOUT ID
  file.link AS Problem,
  pattern AS Pattern,
  status AS Result,
  date_solved AS Date
FROM "02 - Problems" and #problem
SORT date_solved DESC
LIMIT 10
```

## Last 14 days of practice
```dataview
TABLE WITHOUT ID
  file.link AS Day,
  minutes AS Minutes,
  new_problems AS New,
  reviews AS Reviews
FROM "04 - Daily"
SORT date DESC
LIMIT 14
```
