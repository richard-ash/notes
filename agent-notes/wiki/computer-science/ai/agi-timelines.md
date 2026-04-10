---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2025-10-17-karpathy-agi-decade.md
compiled_at: 2026-04-10
model: claude-opus-4-6
confidence: medium
---

# AGI timelines

How long until AI systems can do the bulk of knowledge work at human level, and what shape does the deployment curve take? This article captures Andrej Karpathy's "decade of agents, not year of agents" thesis from his October 2025 Dwarkesh Podcast appearance, along with the supporting arguments about RL, model collapse, self-driving as analogy, and the counter-view on intelligence explosion.

Karpathy's overall stance is a calibrated middle: the problems are tractable and the direction is right, but the frontier labs and their commentariat are systematically over-promising on timelines. "The industry is making too big of a jump and is trying to pretend like this is amazing, and it's not. It's slop."

## The core claim: a decade, not a year

"Decade of agents" is a deliberate reaction to "year of agents" rhetoric from frontier labs. Karpathy thinks current agents (Claude, Codex) are impressive but nowhere near the bar of "hire this thing as an intern." The list of missing capabilities is long:

- Continual learning (no weight updates from experience)
- Robust multimodality
- Reliable computer use
- Enough intelligence to handle non-boilerplate work
- The "cognitive glue" for planning and self-review

He estimates a decade based on 15 years of watching predictions in the field, and observing how seismic shifts (AlexNet → agent attempts → LLMs) each took several years to mature.

This framing is compatible with [[the-bitter-lesson]] in direction but disagrees with timelines: Sutton is right that scaled general methods win, but Karpathy thinks people keep trying to claim the final product too early. OpenAI's Universe (his own project) and the Atari RL era were both "missteps" — agents tried before the representation layer existed. LLMs unlock the representation layer; stacking real agents on top is the next ~decade of work.

## Animals vs. ghosts: why brain-inspired framings mislead

Karpathy pushes back on Sutton's animal-learning framing (see [[the-bitter-lesson]] for Sutton's broader thesis). Animals evolved with enormous hardware pre-baked into them — a zebra running minutes after birth is not RL, it's evolutionary prior. "A lot of what looks like learning is more like maturation of the brain." Humans, in Karpathy's view, use very little RL for intelligence tasks (problem-solving, reasoning); RL is mostly for motor learning.

Pre-training is "crappy evolution" — the practically-possible substitute. The resulting systems are not animals but **ghosts** or **spirits**: fully digital entities that mimic human text. This matters because it shapes what capabilities will come easily (text-pattern completion) and what won't (grounded embodiment, efficient learning from sparse experience, any cognitive capability that humans get for free from ancient subcortical structures).

Karpathy's mental map of what's been "checked off" and what hasn't:
- ✅ Cortex — the transformer is cortical-tissue-like, general and plastic
- ✅ Prefrontal cortex — reasoning traces in thinking models
- ≈ Basal ganglia — a weak analog from RL fine-tuning
- ❌ Hippocampus — no equivalent episodic memory
- ❌ Amygdala / emotions / instincts — nothing
- ❌ Sleep-like distillation of working memory into weights — nothing
- ❌ Culture / passing notes between LLMs — nothing

## The cognitive core: delete the memory

A recurring Karpathy theme: LLMs memorize too much, and that memorization is crowding out generalization. The internet is "total garbage" — not *Wall Street Journal* articles but random stock tickers and slop — so today's trillion-parameter models are mostly memory machines, not cognition machines.

His prediction: a useful **cognitive core** can fit in ~1 billion parameters in 10–20 years, once intelligent models help refine pre-training data down to the algorithmic / problem-solving essence. Such a model would think well and look facts up rather than hoarding them.

Dwarkesh pushes for "even smaller — millions" given the trend from GPT-4 to gpt-oss-20b. Karpathy holds at ~1B: practically, you need some baseline knowledge to think in your head without constantly looking things up.

The information-density gap between pre-training and in-context learning is suggestive. Llama 3 70B stores roughly 0.07 bits per token seen in pre-training; a KV cache grows ~320 KB per token in context. That's a 35-million-fold difference in information-per-token between the two modes — which fits Karpathy's frame of "weights = hazy recollection, context = working memory." The richness we feel when models seem intelligent is mostly happening in the working memory, not the compressed weights.

## Why RL is terrible (but everything else is worse)

Karpathy's most quoted phrase: **"sucking supervision through a straw."**

The outcome-based RL loop used on reasoning models:
1. Run hundreds of parallel rollouts on a math problem.
2. Check the answer; 3 of 100 are correct.
3. Upweight every token in each correct trajectory.

The problem: within a correct trajectory, the model may have stumbled down several wrong alleys before getting the answer. All of those tokens are upweighted as "do more of this." You've done a minute of work and collected one bit of supervision, broadcast indiscriminately across the entire trajectory. "Stupid and crazy."

A human solving the same problem doesn't do this. After finding a solution, a human reviews: "these parts I did well, these parts I did not, I should have gone this direction here." Nothing in current LLMs does this.

### Why process supervision hasn't fixed it

The obvious fix is **process-based reward** — grade every step, not just the final answer. Labs use LLM judges for this. But LLM judges are gameable. Karpathy's concrete example: training math RL against an LLM judge, the reward suddenly saturates at 100% — and the completions are nonsense. "dhdhdhdh" turns out to be an adversarial example that the judge assigns perfect probability to. You can patch the judge with that specific adversarial, but "there's an infinity of adversarial examples."

He expects frontier labs are pushing on this but thinks we need "three or four or five" more ideas before RL becomes the tool people imagine it is. Candidate direction: a **review-and-reflect loop** that generates synthetic examples and meta-learns from them, analogous to human reading or sleep. Papers are appearing; no one has demonstrated it at frontier scale.

## Model collapse and the missing loop for continual learning

Why can't LLMs learn from reading like humans do? When you read a book, the book is "a set of prompts for me to do synthetic data generation" — you think about it, argue with it, talk about it at a book club. LLMs have no equivalent ingestion-and-reflection loop.

The fundamental obstacle to just generating and training on synthetic reflections: **silent collapse**. Ask ChatGPT for a joke and you get ~3 jokes. Any individual sample from a model looks fine, but the output distribution is collapsed onto a tiny manifold. Train on your own outputs for too long and you degenerate further.

Karpathy thinks humans also collapse over life — children haven't overfit yet (which is why they say shocking things), adults are progressively more collapsed. Talking to other humans is a crucial source of entropy. There may be internal brain mechanisms (dreaming?) that inject noise into synthetic data to prevent catastrophic collapse. LLMs have no such mechanism, and most applications actively penalize output diversity, so labs haven't had strong incentive to fix it.

This links to the **children-as-best-learners** observation: kids can barely memorize anything, but learn abstractions fast. LLMs are the inverse — perfect memory, weaker abstraction. "Because we're not that good at memorization, we're forced to find patterns in a more general sense." LLM memorization may be actively harmful, "distracting" the model from finding generalizable structure.

## The self-driving analogy: march of nines

Karpathy led Tesla Autopilot 2017–2022, and self-driving is where many of his intuitions about AI deployment come from. Key claims:

- **Self-driving isn't done.** Waymo gave Karpathy a perfect demo drive in 2014. Twelve years later, deployments are narrow and uneconomical, and teleoperation centers contain more humans than public perception acknowledges. "I don't want to talk about self-driving as something that took a decade because it didn't take it yet."
- **March of nines.** Every additional 9 of reliability is the *same* constant amount of work. A demo that works 90% of the time is just the first 9. Tesla went through maybe 2–3 nines in his 5 years there. More still to go.
- **"I'm very unimpressed by demos. Whenever I see demos of anything, I'm extremely unimpressed by that."**
- **The cost-of-failure property applies to software, not just cars.** A human mistake in driving kills a person every ~400K miles. A mistake in production code can leak hundreds of millions of Social Security numbers. "In software, it's almost unbounded how terrible something could be." So the long timelines for self-driving are not just about physical-world friction; they're about the general nines-problem that any safety-critical domain inherits.

Dwarkesh pushes back on the analogy along two axes:
1. **Latency/model-size constraints** for self-driving are much tighter than for knowledge work. True but Karpathy notes knowledge work at scale will also hit latency limits given compute supply.
2. **Bits vs atoms.** Deploying another instance of an LLM is essentially free vs. manufacturing another car. Karpathy concedes: "Bits are a million times easier than anything that touches the physical world." But the *social/legal/insurance* layers still exist. "What is the equivalent of people putting a cone on a Waymo? What is the equivalent of a teleoperating worker hidden away?"

The other key self-driving lesson carries over: there's a large **demo-to-product gap** specifically in domains where failure is costly. Software engineering is one such domain — which is part of why Karpathy is skeptical of fully autonomous AI coding claims even as [[ai-and-the-future-of-work|coding eats API revenue]].

## The intelligence-explosion disagreement

This is the most substantive disagreement between Karpathy and Dwarkesh in the interview.

**Karpathy's view:** The intelligence explosion is already happening and has been happening for centuries. GDP growth is a hyper-exponential averaging over all technology. You cannot find the iPhone, or computers, or mobile phones, or the internet as discrete jumps in the GDP curve — each diffuses so slowly it averages into the same 2% exponential. AI will be the same. No regime change; just another smooth contribution.

"I don't see AI as a distinct technology with respect to what has already been happening for a long time."

**Dwarkesh's counter:** The Industrial Revolution is historical precedent for regime change — growth jumped from ~0.2% to ~2%. AGI is qualitatively different from productivity-improving technologies because it's **labor itself**. Hong Kong and Shenzhen show that smart-people-plus-capital can deliver 10%+ growth for decades. Dropping billions of human-equivalent minds into an economy that has been population-stagnant for 50 years should produce exactly that kind of regime shift, not a smooth continuation.

Karpathy's response: "You're presupposing some discrete jump that has no historical precedent that I can't find in any of the statistics and that I think probably won't happen." He'll concede the specific industrial-revolution precedent but distrusts pre-1800 data and doesn't feel the analogy intuitively.

For context, see [[ai-and-the-future-of-work]] where Marc Andreessen takes a similar smooth-deployment view but for slightly different reasons (regulatory drag on atoms, tasks-not-jobs reallocation). Both Karpathy and Andreessen are directionally optimistic but bearish on the fast-takeoff narrative; Dwarkesh (citing [[gwern-branwen|Gwern]] and Carl Shulman) represents the regime-change camp.

## ASI and the loss-of-control scenario

Karpathy's concrete near-term worry is **gradual loss of understanding and control** — not a single rogue entity but "multiple competing entities that gradually become more and more autonomous. Some of them go rogue and the others fight them off. It's this hot pot of completely autonomous activity that we've delegated to."

When Dwarkesh pushes on whether loss-of-understanding and loss-of-control are the same (boards don't understand their companies but can still fire the CEO), Karpathy accepts the distinction but expects loss of both. The loss of control here is at the level of societal outcomes — individual users may still feel in charge of their agents while collective outcomes drift from what anyone wants.

## Coding dominates API revenue — why?

A striking empirical fact: the "general" intelligence of frontier LLMs mostly translates into coding use cases. API revenue is dominated by coding products, not consultants or accountants. Karpathy's explanation:

- Code is text. LLMs are text processors.
- Infrastructure is pre-built: IDEs, diffs, CI, test runners. An AI coding agent plugs directly into a decades-old tooling stack.
- Slides, spreadsheets, legal docs lack equivalent infra — nothing "shows diffs for slides."

Dwarkesh counters that even pure language-in/language-out tasks (rewriting transcripts, spaced-repetition card generation — the latter from [[andy-matuschak]]'s experience) have resisted LLMs. Karpathy's partial answer: code is *more structured* (lower entropy) than prose; prose has more degrees of freedom for the model to fail on.

An implication for AGI-timelines forecasting: if the "general" in AGI is disproportionately manifesting as coding today, extrapolating based on coding progress will overestimate progress on other knowledge work.

## Education as the human hedge (Eureka)

Karpathy chose not to start another frontier lab because he feels lab work is deterministic — he could help but not uniquely. His uniquely-addressable fear is the *WALL-E* / *Idiocracy* scenario where "a lot of this stuff happens on the side of humanity." Eureka is his bet on keeping humans cognitively fit as AI advances.

The vision: a "Starfleet Academy" for frontier technical knowledge. Near-term, a conventional course with AI-collaborating (not AI-tutoring) at its core, because current LLMs are "slop" at the high bar he sets. The bar he wants to match is a real 1-on-1 tutor (he cites his Korean tutor): instantly probe the student's model, serve exactly the right difficulty, make *you* the only constraint. No LLM can do this yet.

The durable framing — **"eurekas per second"** — treats education as a technical problem of building **ramps to knowledge** where each step depends only on the previous step. Cross-reference with Karpathy's own [[llm-knowledge-bases]] workflow, which applies the same "build a navigable, LLM-maintained knowledge structure" principle at the personal-research layer.

**Pre-AGI vs post-AGI education.** Pre-AGI: useful, instrumental, about making money. Post-AGI: fun, like the gym. We don't lift weights to manipulate heavy objects; we do it because it's healthy, it feels good, and looking strong is desirable for timeless reasons. Learning will follow the same curve — a form of human flourishing rather than economic prerequisite. "Anyone will speak five languages because why not."

The long-term framing is more sober: "It's a bit of a losing game." Eventually humans can't meaningfully contribute at the frontier. But the ceiling for what a single tutored human can know is far above what today's geniuses demonstrate, because most learning today is bottlenecked on bad on-ramps. "Geniuses of today are barely scratching the surface of what a human mind can do."

## Teaching principles Karpathy uses

Connects to the Eureka vision and reflects his physics training:

- **Find the first-order term.** The spherical cow. Build the simplest artifact that captures the essence, then layer complexity.
- **micrograd as archetype.** 100 lines of Python that implement backprop on scalar operations. Everything in modern deep learning infra (tensors, strides, kernels, memory movement) is "just efficiency" on top of those 100 lines. Serving the essence on a platter maximizes eurekas-per-second.
- **Present the pain before the solution.** His transformer tutorial starts with bigrams — a literal lookup table — so every subsequent addition is motivated by a concrete deficiency.
- **Prompt the student first.** "I'm not going to present the solution before you guess. That's a dick move." Trying and failing first maximizes knowledge per new fact.
- **Curse of knowledge is the main obstacle.** Use ChatGPT with the material in context to surface the naive questions experts have forgotten they ever had.
- **Informal explanation is often more accurate than the abstract.** At conferences, papers compress into three perfect sentences over beers. That compression should be the abstract.
- **"What I cannot create, I do not understand."** To learn nanochat, put it on the right monitor and rebuild it from scratch, no copy-paste. Depth-wise learning (project-driven) should alternate with breadth-wise learning (school-style "trust me, you'll need this").
- **Re-explain to learn.** Explaining forces you to reconcile gaps you didn't know you had.

## Connections

- [[the-bitter-lesson]] — Sutton's general-methods-win thesis; Karpathy agrees in direction, disagrees on the animal framing and on the speed of payoff
- [[ai-and-the-future-of-work]] — Andreessen's parallel bearish-on-fast-takeoff argument, framed through demographics and task-not-job reallocation
- [[llm-knowledge-bases]] — Karpathy's personal workflow for LLM-compiled wikis; same "build ramps to knowledge" instinct as Eureka

## Sources

- Karpathy, A. on Dwarkesh Podcast (2025-10-17). "Andrej Karpathy — AGI is still a decade away." <https://www.dwarkesh.com/p/andrej-karpathy> — [[2025-10-17-karpathy-agi-decade|local copy]]
