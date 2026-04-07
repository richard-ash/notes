---
name: book-interview
description: Interview about a book you just finished, then compile your answers into a structured book note in books/catalog/.
allowed-tools: Read Write Edit Glob Grep AskUserQuestion
argument-hint: "[book title]"
---

Conduct a conversational interview about a book, then write a structured note.

**Input:** $ARGUMENTS (book title, or empty — ask if missing)

## Setup

1. Read the template at `books/catalog/template.md` to understand the target structure.
2. If no book title was given, ask for it.
3. Determine the slug: lowercase, hyphenated title (e.g., "how-to-feed-the-world").
4. Check if `books/catalog/<slug>/index.md` or `books/catalog/<slug>.md` already exists. If so, tell the user and ask whether to overwrite or update.

## The Interview

Ask questions **one at a time**, waiting for the user's response before moving on. Keep the conversation natural — follow up on interesting points, ask for clarification, push gently for specifics. You are a thoughtful reader having a book discussion, not a form to fill out.

The interview has two phases:

### Phase 1: Metadata (ask together in one message)
- Who's the author?
- When did you finish it? (default to today if they say "just finished")
- What genre or category would you put it in?
- Rating out of 5?

### Phase 2: Substance (one question at a time)
Work through these in order, but adapt based on their answers. Skip or combine questions if the conversation flows naturally into them. Follow up when something is interesting.

1. **Classification** — "What kind of book is this? How would you describe it to someone?"
2. **The sentence** — "If you had to describe the whole book in one sentence, what would it be?"
3. **Structure** — "How is the book organized? What are the major parts and how do they build on each other?"
4. **The problem** — "What question or problem is the author trying to address? Do you think they succeeded?"
5. **Key terms** — "What are the key terms or concepts the author introduces? Any frameworks or vocabulary that stuck with you?" (e.g., "Hamiltonian vs Jeffersonian" in Why Nothing Works)
6. **Key ideas** — "What are the most important arguments or insights? What did the author get right?" (This one often has the most to say — let it breathe, ask follow-ups.)
7. **Disagreements** — "Where do you disagree with the author, or where do you think the argument is weakest?" (Skip for narrative/descriptive books that aren't making an argument — write "Not applicable" in the note.)
8. **Takeaways** — "Did this change how you think about anything? Will you do anything differently?"
9. **Connections** — "How does this connect to other books you've read or things you've been thinking about?"
10. **Memorable passages** — "Any quotes or passages that stuck with you?" (Optional — skip if they don't have any top of mind.)
11. **Highlights** — "Do you have Kindle highlights or other highlights you want included?" If yes, ask for the file path or pasted content.

After the last question, let them know you're going to compile the note.

## Compilation

1. Synthesize the interview into a book note following the template structure. Use the user's own words and phrasing where possible — don't over-polish or add things they didn't say. Clean up for readability but preserve voice.
2. Fill in the frontmatter from Phase 1 answers.
3. Write the note to `books/catalog/<slug>/index.md` (create the directory).
4. **If highlights were provided:** parse them into `books/catalog/<slug>/highlights.md`, organized by chapter. Include any user notes/annotations alongside the highlights. The index.md Memorable Passages section should link to the highlights file: `See [highlights](highlights.md) for all highlights organized by chapter.`
   - Kindle HTML exports: extract text from `.noteText` divs, section headings from `.sectionHeading` divs, and user notes from entries preceded by `Note -` headings. Format highlights as blockquotes (`>`), user notes as italicized (`*Note: ...*`).
   - Plain text or other formats: preserve the highlights as-is, organize by chapter if structure is apparent.
5. If the book isn't already listed in `books/index.md`, add it under the appropriate heading (create a new heading if needed). Use a plain markdown link: `- [Book Title](books/catalog/<slug>/index.md)`.
6. Show the user the compiled note and ask if they want any changes.

## Key rules

- This writes into `books/` (personal notes), not `agent-notes/`. This is authorized for this skill.
- Use plain Markdown links, not `[[wikilinks]]`.
- Keep the user's voice. Don't editorialize or add analysis they didn't express.
- If they mention highlights they've already captured elsewhere, ask if they want those included.
- Commit style if asked to commit: short imperative subject, no body, no `Co-Authored-By`.
