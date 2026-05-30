---
project_status: active
area:
due:
outcome:
type: project
created:
---
<!-- Live sections need the Dataview plugin; without it the assistant keeps them as hand-updated lists. -->

## Outcome
What "done" looks like.

## Tasks
Add tasks here directly — **or capture them anywhere** (e.g. today's daily note) with a `[[link to this project]]`; they surface below.
- [ ]

### ⤵ Captured elsewhere (open tasks linking this project)
```dataview
TASK
WHERE !completed AND contains(outlinks, this.file.link)
SORT due ASC
```

## People
-

## 🔗 Linked notes & resources
```dataview
LIST
WHERE (type = "note" OR type = "resource") AND contains(file.outlinks, this.file.link)
SORT file.mtime DESC
```

## Log
-
