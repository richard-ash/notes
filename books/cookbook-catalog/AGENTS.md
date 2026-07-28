# Cookbook catalog

One note per cookbook: a checklist of every recipe in the book, checked off as
Richard cooks them. `index.md` lists them all.

## Template

```markdown
---
title: "Full Title: Including Subtitle"
author: "Author Name"
---

# Full Title: Including Subtitle

## Chapter Name As Printed

- [ ] Recipe Name
- Produce or Ingredient Category      <!-- no checkbox: it's an index, not a recipe -->
  - [ ] Recipe Under That Category
```

## Rules

- Chapter order and recipe order follow the book. No page numbers, no descriptions.
- Only real recipes get a checkbox. Table-of-contents entries that are just an index
  over sub-recipes become plain bullets with the recipes nested beneath.
- Skip generic technique entries ("Boil", "Roast", "Sauté").
- Never change an existing `- [x]` — those are Richard's cooking records.
- Add the note to `index.md`, alphabetized by title.
