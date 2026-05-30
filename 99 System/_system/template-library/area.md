---
type: area
created: 
area_status: active
---
<!-- This note is the AREA DASHBOARD — an at-a-glance index of everything in this area.
     Queries below are live with the Dataview plugin (config.md → dataview: true).
     If dataview is off, the assistant maintains these as hand-updated lists instead.
     Everything works by the `area` field on each object pointing back to this note. -->

## Purpose
_What this domain of life is about, in a line._

## ✅ Open tasks here
```dataview
TASK
WHERE !completed AND area = this.file.link
SORT due ASC
```

## 🚧 Active projects
```dataview
TABLE project_status, due
WHERE type = "project" AND area = this.file.link AND project_status = "active"
SORT due ASC
```

## 🗓 Upcoming
```dataview
TABLE date, with
WHERE type = "event" AND area = this.file.link AND date >= date(today)
SORT date ASC
```

## 👤 People
```dataview
LIST
WHERE type = "person" AND area = this.file.link
```

## 📝 Recent notes & resources
```dataview
LIST
WHERE (type = "note" OR type = "resource") AND area = this.file.link
SORT file.mtime DESC
LIMIT 10
```

## Notes
_Free-form context about this area._
