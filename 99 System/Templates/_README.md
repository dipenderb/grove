# Templates

This folder holds one note template per object **type you actually keep** — nothing else.

It ships **empty by design.** Onboarding (and the `new-object-type` skill) populate it: for every kept type, a template is copied from the internal reference set in `99 System/_system/template-library/` and adapted, or generated fresh for a custom type. So you only ever see templates for types that exist in *your* OS — no unused scaffolding.

The reference set in `_system/template-library/` is machinery (hidden); this folder is what Obsidian's Templater/Templates plugin inserts from.
