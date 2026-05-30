---
full_name:
area:
relationship:
role:
org:
email:
phone:
type: person
created:
---
<!-- Live sections need the Dataview plugin; without it the assistant keeps them as hand-updated lists. -->

## Context
Who they are and how you know them.

## 🗓 Events & meetings
```dataview
TABLE WITHOUT ID file.link AS Event, date
WHERE type = "event" AND contains(with, this.file.link)
SORT date DESC
```

## 🔗 Linked from
```dataview
LIST
WHERE contains(file.outlinks, this.file.link) AND file.path != this.file.path
SORT file.mtime DESC
LIMIT 15
```

## Open with them
Add directly — **or capture anywhere** with a `[[link to this person]]`; they surface below.
- [ ]

### ⤵ Captured elsewhere (open tasks linking this person)
```dataview
TASK
WHERE !completed AND contains(outlinks, this.file.link)
SORT due ASC
```
