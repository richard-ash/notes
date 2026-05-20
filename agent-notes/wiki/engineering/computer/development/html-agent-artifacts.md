---
source: agent
compiled_from:
  - agent-notes/raw/engineering/computer/development/2026-05-18-html-as-ai-specs.md
compiled_at: 2026-05-20
model: claude-opus-4-7
confidence: medium
---

# HTML as the artifact medium for human-agent collaboration

Thariq Shihipar, an engineer on Anthropic's Claude Code team, argues that as agents have lengthened from 50-line one-shots into hour-long sessions, **Markdown has quietly stopped working as the human-agent communication medium** — not because the models can't read it, but because the humans can't. A thousand-line plan in Markdown is a wall of text the operator skims at best and asks Claude to edit at worst. The proposed replacement is HTML: rendered, scrollable, mockup-rich documents that the human actually *reads* and engages with, which keeps the human in the loop on what the agent is doing.

The slogan Shihipar offers is "HTML is the new Markdown." The underlying claim is that the right format depends on who is reading the artifact, and for plans and specs the binding constraint is now human engagement, not parser simplicity.

## The compute allocator mindset

Shihipar's framing for why specs matter more (not less) as models improve:

> "When you say, 'Okay, Claude can run for 8 hours,' what you're really saying is Claude can spend like 500 bucks. All of us are becoming these compute allocators now. So you have to decide what is worthwhile spending the compute on."

This is the same observation as Claire Vo's "you're a compute allocator, babe" framing of post-PM work: the humans' job has moved up the stack from typing implementations to deciding what the implementation should be. The artifact that captures the decision is the spec/plan, and its quality bounds the quality of the $500-of-compute that's about to be spent.

The compute-allocator mindset is the durable contribution beneath the format choice. It's why Shihipar can simultaneously say "models are smarter" and "plans matter more than ever" — these are not in tension once you reframe the human's role from implementer to budget-deployer. Connects to [[judgment-in-ai-assisted-development|judgment-in-ai-assisted-development]] (Larson's constraint hierarchy: time → attention → judgment → creativity; compute-allocation is judgment scaling) and [[agentic-engineering|agentic-engineering]] (Karpathy's taste-as-bottleneck thesis at a different framing).

## Why Markdown stopped working

Shihipar's read of the failure mode is concrete:

- **Read decay.** "A thousand-line markdown file, I don't even edit them anymore. I just have Claude edit them instead." Once the human is no longer reading the plan, they're no longer in the loop, and the agent loses the human oversight the long-running session was supposed to be deploying.
- **ASCII-art compensation.** Models try to compensate for Markdown's expressive limits with ASCII mockups that "try really hard." HTML lets the model spend the same tokens drawing actual visual things rather than approximating them in text.
- **No richer affordances.** Mockups, tabs, interactive elements, comments — none of these exist in Markdown. They all exist in HTML by default, at no extra prompting cost.
- **One-shot screen ceiling.** Shihipar's rule of thumb for brainstorming: "I'm not going to read a longer output than the screen on Claude Code." Eight Markdown ideas blow past one screen and the operator only sees the first two. Eight HTML cards in a scrollable rendered page get scrolled through.

The point is not that HTML is *more efficient* — it costs more tokens — but that the human-engagement gain is worth the token cost, because the engagement is the loop-closing that justifies the agent run in the first place.

## Five applications Shihipar walks through

The transcript steps through specific uses, each of which shows a different reason HTML is the better medium:

### 1. Brainstorming with mockups

Prompt: *"Brainstorm me some ideas in an HTML file."* The output is a rendered page with cards for each idea, each card containing a name, description, visual mockup, and a "risk" line. The operator scrolls eight options instead of skipping past them; the mockups make the abstractions concrete enough to pick from.

### 2. Implementation plans

Prompt: *"Create an HTML file as a plan that helps me visualize what the implementation plan is. Include excerpts, mockups, code, whatever is needed to give me maximum context."* The output includes a file system tree, an excerpt of the skill.md, a mood board, example components, helper script signatures — all rendered visually. Shihipar's comment: "This is something I will actually read." This is the spec-as-artifact use that parallels [[spec-driven-development|spec-driven-development]]'s workflow, but at the format layer rather than the workflow layer (see [Relationship to spec-driven development](#relationship-to-spec-driven-development) below).

### 3. Throwaway micro-UIs for specific decision points

When Shihipar didn't like a section of the plan (a table of CSV-rendering decision rules), instead of editing in the terminal he prompted: *"Create an editable HTML artifact. Make this a custom UI that helps me with structure but gives me flexibility. Design the ideal interface for this problem."* Claude generated a bespoke interface with editable fields, hide/copy controls, the ability to add new fields, and a "copy back as markdown" output. Shihipar pastes the result into the plan.

Vo's reframing of what's happening: *"This is not even personal software. This is micro-software on top of micro-software. You've made a personalized plan, then you're taking a module in the personalized plan and zooming into it using a very custom UI."* The interaction model is throwaway agent-generated UI for one specific human decision — disposable software that exists only to elicit higher-quality human input.

### 4. Living design systems

Shihipar maintains a single `designsystem.html` file representing his design system (colors, typography, spacing, radius, core components). He passes it from project to project the way teams used to pass around `design.md` files, except this one renders. Vo's advanced variant: extract a design system from both a marketing repo and an app repo (the same system has subtle expressions in each), build a "component visualization page" that shows the components in action, and use it as a source of truth for marketing (download transparent PNGs for decks/videos) as well as for code.

The slogan: "Design.md is dead. Long live design.html."

### 5. Status updates to managers

Shihipar sends his weekly status report to his manager (Cat) in HTML rather than Markdown. The construction is automated — he gets Claude to read his Slack and produce the report — but the medium choice is deliberate: "She actually gets to read it, and I don't have to spend that much time on it." Vo frames this as "the new internal competition: who is building the best product to represent themselves to the manager."

The structural point is that internal communication is no longer cost-bounded by content production: the marginal cost of a rendered, well-organized HTML page is the same as the marginal cost of a bulleted Markdown list. Once production cost goes to zero, the format that wins is the one that gets *read*.

## Prompting philosophy: trust + an out

Shihipar's prompts are strikingly simple. The full implementation-plan prompt was: *"Create an HTML file as a plan that helps me visualize what the implementation plan is. Include excerpts, mockups, code, whatever is needed to give me maximum context."* Vo points out it even contains a typo (`excerpts` misspelled) and Claude produces a rich, well-organized plan anyway.

Two prompting patterns worth keeping:

- **Specify the must-haves; give Claude an out for the rest.** Shihipar wanted code excerpts and was unsure Claude would include them, so he named them explicitly. But he ended with "whatever is needed to give me maximum context" — his stated translation: *"Hey Claude, I trust you here. I want to just be in the loop with you."*
- **Don't over-constrain via skills.** "Sometimes when I see people with a lot of over-built skills like 'you're an expert planner or something,' that is usually outsourcing too much and constraining it." The same principle as [[claude-code-skills|skills]] design — progressive disclosure beats elaborate persona priming.

Connects to [[spec-driven-development|spec-driven-development]]'s anti-default prompting moves ("explain it like I'm 5" and "you're wrong, defend your argument") — different specific moves, same underlying orientation of treating the agent as a colleague who needs intent and an out, not a script and a cage.

## Just-in-time documentation and the abundance mindset

Shihipar's framing of what becomes possible when artifact production cost drops to zero:

> "I think when all of that cost goes to functionally zero, you can up-level the things that you should care about — which is, what is the content of the plan? Is it a good idea? Do we feel like it's going to be executed well? As opposed to: I can't put an interactive markdown document in our blessed document repository, so I have to have another asset somewhere else."

This is the "just-in-time documentation" thesis: high-quality, custom-format, throwaway artifacts produced for the moment they're needed, rather than templated artifacts shoehorned into a centralized repository. The executive objection ("what if we can't find this again?") gets answered by "Claude can find it for us" — an assumption that agentic search can substitute for human-curated taxonomy.

Vo's gloss: "Creating content was relatively expensive, consuming it was expensive, finding it was hard. When all of that cost goes to functionally zero, you can put stuff wherever in whatever format because we know these models are very good at using tools to discover the context that they need."

The implication for documentation practice is that the centralized-knowledge-base model (one source of truth, one template, one location) becomes optional once distributed-artifact-plus-agent-retrieval becomes a substitute. The tradeoff is durability vs. fit-to-purpose: a centralized doc lasts; a custom HTML artifact is the right shape for the specific decision but probably gets discovered by an agent rather than a human the next time it's needed.

## Relationship to spec-driven development

This sits one layer deeper than [[spec-driven-development|Nystrom's spec-driven development]]. Nystrom describes the *workflow* (write a comprehensive spec, hand to Codex, agent builds, spec is the source of truth); Shihipar describes the *artifact format* (HTML, not Markdown). They are compatible — you can do spec-driven development with HTML specs — but they answer different questions:

- Nystrom's question: *How do I structure the human-agent contract so the agent can one-shot?* Answer: spec + code pointers + verification protocol + CLI for self-verification.
- Shihipar's question: *What format should the artifacts I exchange with the agent take?* Answer: rendered HTML when richness pays for engagement; Markdown when it doesn't.

A combined practice would write Nystrom's spec in Shihipar's format: an HTML file checked into the repo, with code pointers + verification protocol embedded, that the human actually reads when reviewing changes. The combination removes the failure mode Shihipar names ("I stopped reading the plan, so I stopped being in the loop") from Nystrom's workflow, which otherwise inherits the Markdown-read-decay problem at scale.

The contrast also surfaces a tension: spec-driven development emphasizes that **the spec is durable and version-controlled** (history of the spec is the change log of how the feature behaves). Shihipar's just-in-time-documentation framing emphasizes that **artifacts are throwaway**. The reconciliation: the spec for a long-lived feature is durable; the throwaway micro-UI used to elicit a single human decision during planning is not. Both can be HTML; only one is checked in.

## Cross-connections

- [[spec-driven-development]] — Nystrom's workflow describes spec-as-source-of-truth; Shihipar adds the format dimension. Combined practice writes spec-driven workflows in HTML rather than Markdown.
- [[claude-code]] — Shihipar is on the Claude Code team; his HTML practice is emergent within that team. The compute-allocator framing is a generalization of Cherny's session-management principles for longer-running agents.
- [[agentic-engineering-architecture]] — Tan's fat-skills/fat-code/thin-harness model treats Markdown as the canonical fat-skill medium. Shihipar's experience suggests the format choice within "fat" is itself a design variable: HTML is a richer fat-skill for human-loop artifacts; Markdown remains the right choice for skills the agent reads alone.
- [[agentic-engineering]] — Karpathy's taste-as-bottleneck thesis predicts that the human-readable artifact format becomes the binding constraint as models scale, which is the same observation Shihipar makes empirically.
- [[judgment-in-ai-assisted-development]] — Larson's hierarchy puts judgment as the new scarce resource. The compute-allocator mindset is judgment-scaling: high-quality plans are what convert agent-compute into useful output.
- [[claude-code-skills]] — Shihipar's caution about over-built skills ("you're an expert planner") aligns with Anthropic's published skill-design guidance (progressive disclosure, don't over-prime).
- [[unattended-coding-agents]] — Stripe's Minions and Notion's [[spec-driven-development|Boxy]] both produce PRs with screenshots/preview-URLs for human review. The HTML-artifact pattern is the same engagement-quality optimization applied to the planning side of the workflow, before the agent runs.

## Caveats

The talk is one engineer's emerging practice, not an evaluated workflow. Specific claims worth flagging:

- **Token-cost tradeoff is unmeasured.** HTML artifacts cost more tokens than Markdown equivalents. Shihipar asserts the engagement gain is worth it but doesn't quantify either side.
- **The "Claude can find it" assumption is load-bearing.** The just-in-time-documentation thesis requires that agent-retrieval is a working substitute for human-curated taxonomy. This holds for personal-scale practice but is unproven at org-scale where retrieval has to span teams, time, and access controls.
- **Collaboration story is thin.** Shihipar's main collaboration use is uploading HTML to a web host and sharing the link. That works for read-mostly artifacts (status reports, design systems) but doesn't yet have a comment/review workflow at parity with Google Docs or GitHub PRs. Vo's comment-overlay-on-HTML-plan idea is presented as future work, not extant tooling.
- **Format choice is not monotonic.** Shihipar isn't claiming Markdown is dead in general — agent-only artifacts (skills, configs, tool definitions) still work fine as plain text. The argument is specific to artifacts the human reads.

## Sources

- Thariq Shihipar and Claire Vo (2026). "Why this Claude Code engineer uses HTML files as AI specs." *How I AI* podcast, YouTube. <https://www.youtube.com/watch?v=Qrpm7E80wQ0> — [[2026-05-18-html-as-ai-specs|local copy]]
