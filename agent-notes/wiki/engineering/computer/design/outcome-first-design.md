---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/design/2026-09-23-skip-the-tools-make-the-outcomes.md
compiled_at: 2026-09-24
model: claude-fable-5-1
confidence: medium
---

# Outcome-First Design

**Outcome-first design** is Luke Wroblewski's name for inverting the default software instinct: instead of shipping a tool that a person learns and operates to produce a result, ship the result directly and offer the tool afterward as a drill-down. His slogan is "skip the tools, make the outcomes," and his diagnostic question for any product is: *are you building another tool, or delivering the outcome the tool was supposed to produce?*

## The argument

Wroblewski's premise is that decades of software practice have implanted a "tool first, outcome second" reflex. The profession got very good at designing tools (report builders, video editors, IDEs) that, once learned, let people create things. A tool was always only a means to an end. His observation is that most current AI work reproduces that reflex at higher speed: it builds more of the same tools, faster. But if a model can take a person straight to the end state, the tool becomes an optional intermediate rather than the product.

Two examples anchor the claim, both from his own products:

- **Exposit**, an AI-run newsroom he built around 2024. Agents did the curating, writing, and editing; the team then presented the output as a conventional news site with headlines, sections, search, and navigation. In his words, they had built "a news tool, like all the other news sites out there, just run by AI." When they added a feature that compiled a personalized report on any topic the reader asked about, drawing on latest coverage, related events, people, and places, that feature quickly became the dominant way people used the site. Readers started from the answer and only then, if they wanted, dropped into articles, entities, and sources.
- **Ask LukeW**, the conversational interface to his own writing. Originally it showed nothing until you typed a question. He now runs a daily job that gathers his latest tweets, articles, and files and compiles a "what's Luke thinking about now" answer, so visitors get something to read before asking anything. He frames this as starting with an answer instead of requiring a question.

## Just-in-time content

The Exposit report is an instance of what Wroblewski calls **just-in-time content**: material generated in real time, for a specific person, with a specific need, at a specific moment. The contrast is with publishing, where you write something once and hope it fits everyone who arrives. The just-in-time alternative is to maintain a corpus that can be recombined endlessly and let each request assemble its own timely answer.

This is the same architectural bet as [[llm-knowledge-bases]]: the durable asset is a well-maintained corpus, and the "article" a reader sees is a view compiled on demand rather than a fixed document. Wroblewski's contribution is to push that pattern into the interface layer. The corpus is invisible; the compiled outcome is the front door.

## Why this matters now

Read alongside [[decide-execute-deliver-sandwich]], the tool is the interface to the *execute* layer of knowledge work. Tools exist because a human had to perform the middle step and needed affordances to do it. If an agent absorbs execution, the interface built for human execution loses its reason to exist, and what remains is deciding what you want and receiving it. Wroblewski's inversion is a design-side consequence of the same compression that Narayanan describes on the labor side.

It also rhymes with [[outcome-based-pricing]]. Bret Taylor argues AI products should charge for labor delivered rather than seats or usage; Wroblewski argues they should *present* the labor delivered rather than the workbench. Pricing the outcome and designing for the outcome are two faces of the same shift from tool vendor to result provider.

Within this domain, [[design-process-ai-era]] describes engineering velocity dismantling the traditional design pipeline. Outcome-first design is a candidate answer to "what do designers do instead": decide which outcome to deliver unprompted and how to let people drill from the answer back into the underlying material.

## Implications and open questions

These are extrapolations from the essay, not claims Wroblewski makes.

- **Progressive disclosure runs backward.** Classic progressive disclosure starts with a simple tool and reveals complexity on demand. Outcome-first starts with the finished artifact and reveals the tool on demand. The Exposit report with drill-down to sources is exactly this: the answer is the top level, the newsroom is the detail.
- **The blank-prompt problem is a tool-first symptom.** An empty text box asks the user to know what to want. Ask LukeW's daily digest sidesteps it by guessing well. This suggests that a default, unprompted outcome is often more valuable than a more powerful query interface.
- **Trust moves from the process to the output.** A tool lets a person watch and steer each step, which is how they come to trust the result. An outcome arrives finished. Outcome-first products therefore need a path back to evidence (Exposit's links to articles and sources) or they trade usability for unverifiable claims.
- **Tools survive where the outcome is not yet known.** Exploratory work, where the person is discovering what they want by manipulating material, still needs a tool. The inversion is strongest when the desired outcome is legible up front (a report, a briefing, a summary) and weakest when the value is in the manipulation itself.
- **It generalizes beyond content.** The same question applies to dashboards (deliver the decision, not the chart), analytics (deliver the anomaly, not the query builder), and internal tooling. The test is whether the person wanted the artifact or wanted the ability to make artifacts.

## Sources
- Luke Wroblewski (2026). "Skip the Tools, Make the Outcomes." <https://www.lukew.com/ff/entry.asp?2163> — [[2026-09-23-skip-the-tools-make-the-outcomes|local copy]]
