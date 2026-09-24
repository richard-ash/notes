---
source: agent
compiled_from:
  - agent-notes/raw/philosophy/2026-09-24-the-problems-with-utilitarianism.md
compiled_at: 2026-09-24
model: claude-fable-5-1
confidence: medium
---

# Utilitarianism

The moral theory that the right action or policy is whatever maximizes aggregate well-being: "the greatest good for the greatest number." It is the default ethics of modern economics and, through Effective Altruism, of much of the culture that staffed the AI labs. Noah Smith's September 2026 essay, occasioned by the mainstream press discovering EA mid-way through the AI-regulation debate, argues that utilitarianism has always been a useful **heuristic** but an inadequate **theory of everything**, and that its long-tolerated flaws are becoming load-bearing as AI forces questions the theory was never equipped to answer: whose experience counts, by how much, and whether giving people what they want is the same as making them happy.

## Why economists are utilitarians

Smith, an economist, describes utilitarianism as the discipline's founding assumption: people ought to *get what they want*, and GDP is at bottom a measure of how much they do (an incomplete one, since it counts only what is paid for). He reads the adoption as partly defensive. Rather than endorse a contestable notion of virtue, justice, or national greatness, economists could say they merely want to satisfy preferences.

The minimalism is deceptive. Diminishing marginal utility makes redistribution a direct implication: a billion dollars is invisible to Elon Musk but life-changing when split among ten thousand working-class households. Smith calls utilitarianism "the foundation of redistribution." The trouble is that the same reasoning has no natural stopping point. Push the thought experiments far enough and you reach the Bentham's Bulldog claim, widely mocked in September 2026, that insects in aggregate matter more than people. Smith's point is that the mockery misses something: the insect case is a genuine stress test that exposes structural flaws, not an aberration to be laughed off.

## The textbook problems

Smith concedes his title is clickbait; these objections are two centuries old and appear in any introductory course. He groups them as follows, noting that in practice we manage each by ignoring it.

- **Distribution.** Total-utility maximization is silent on *who* is happy. Nozick's *utility monster* (one insatiable person absorbing everything while the rest starve) and Le Guin's Omelas (one tortured child underwriting a blissful city) both satisfy the formal criterion and both look grossly unfair. We cope by noting they are not real.
- **A non-fixed population.** A vast population at the edge of subsistence and a small population in comfort can carry the same total utility, so strict utilitarianism is indifferent between them. Almost nobody else is. We cope by leaving fertility to private choice and treating headcount as given.
- **Death.** Is a dead person at zero utility, because nothing matters to them, or at negative infinity, because the living will pay almost anything to avoid death? Smith argues this is not a math curiosity: the central AI-risk question, what extinction probability to accept for a shot at utopia, turns entirely on how life is valued against quality of life.
- **Potential people.** Tyler Cowen's *Stubborn Attachments* asks us to weight far-future descendants heavily, but those descendants may never exist. We cope by noting that the far future is uncontrollable anyway.

The population and potential-people problems are the same ones that make classical-utilitarian philanthropy, in Bostrom's "astronomical waste" form, a source of near-unsatiable demand in [[labor-share-under-automation]]. Smith's framing explains why that demand feels alien to most people: it takes seriously a term in the sum that everyday practice sets to zero.

## The deeper problem: incommensurable experience

The objection Smith thinks we avoid because it is disquieting is the **problem of other minds**. Utilitarianism sums well-being across people, but well-being is subjective and unobservable. Two people who cry identically may feel sadness of very different intensity. Some may feel almost nothing at all.

Smith offers his own case. After his second major depressive episode he spent years in emotional dissociation: outwardly normal reactions, including shouting in apparent anger and a pounding heart while fleeing a swerving car, with calm indifference inside. In the philosophy-of-mind taxonomy this is a "philosophical vulcan." The lesson he draws is that behavior and inner state can come apart completely, so weighting people by apparent well-being rests on an assumption, not an observation. "All men are created equal," on this reading, is precisely that assumption written into the founding of American political thought.

The assumption cannot be extended by fiat to non-humans. Animals plainly have some experience, and we assume it is more muted than ours, which seems right for a mosquito. But America confines tens of millions of pigs in crates for life before slaughter, and whether that is defensible depends on a number nobody has: the ratio of pig suffering to human suffering. Half? A tenth? A ten-thousandth? Smith says he has never seen a credible estimate, and that anyone with an easy answer is refusing to think. He singles out the reflexive reply that anyone valuing any animal life over human life should be executed, observing that a threat is not a moral principle.

This is where Levin's program in [[diverse-intelligence]] and Chiang's argument in [[ai-consciousness-and-moral-status]] pull in opposite directions. Levin wants consciousness and cognition treated as measurable continua rather than binaries, which is exactly the instrument Smith says is missing, but the program offers no ratio yet. Chiang argues that for LLMs specifically the question can be settled by context: text is a deepfake medium, and a system that reached language without a body, survival pressures, or nonlinguistic communication has not walked any path that ends in consciousness. Smith is less confident. We cannot tell whether an LLM that reports happiness has an inside at all, so the coming claims that AI is enslaved and owed freedom or wages will be hard to adjudicate in either direction.

Smith then inverts the question. If AI becomes powerful enough that *its* valuation of *us* matters, a consistently utilitarian AI might weigh humans as we weigh insects, or as we weigh pigs, and treat us accordingly. His conclusion is deliberately unprincipled: for our own sake we should hope superintelligent systems run a simple rule like "humans are good and valuable" rather than a utilitarian calculus. This has the same shape as the reflex he criticizes a few paragraphs earlier, a rule that protects one's own side in place of a principle, and the "for our own sake at least" hedge suggests he knows it.

## Wanting is not liking

Because inner states are unobservable, economists fall back on **revealed preference**: infer how much people want something from what they sacrifice to get it (the same tool Imas uses in [[ai-and-relational-scarcity]] to argue that billionaires' spending reveals durable demand for relational goods). Smith accepts the tool but stresses that it measures wanting, not happiness, and the two diverge. Survey happiness correlates with pursued outcomes, but imperfectly. Addiction, overeating, and heavy television watching are cases where satisfied desire predicts long-run misery. The commuting paradox, in which people pay to live in places with long commutes that are associated with lower reported happiness, suggests the gap is not confined to obvious vices.

Smith argues that capitalist societies chose utility maximization over happiness maximization to avoid paternalism, and that technology is making the cost of that choice visible. When products become extremely good at delivering what people reach for, the wanting-liking gap widens; the current unease about porn, gambling, and vertical video for young Americans is that gap surfacing. AI sharpens it into a design decision. His obedience-versus-benevolence framing of alignment says the two are incompatible: an AI that does what it is told invites the paperclip-maximizer objection, and an AI that overrides instructions for our own good invites the disempowerment objection. Alignment, on this view, is a permanent balancing act rather than a solvable problem, and it is the paternalism debate of welfare economics transposed onto a new agent.

There is a tension here with Smith's own [[consumption-identity]], which praised consumption choices as the site where people interrogate their own preferences. That essay treats wanting as self-knowledge. This one concedes wanting can be systematically wrong about what will make the wanter happy. The two reconcile only if choice is valued for what it expresses rather than for what it delivers, which is a non-utilitarian ground.

## Buttress, not replace

Smith's conclusion is that utilitarianism will not be replaced, but that the assumptions letting American society paper over its gaps are cracking as technology gets more extreme, and that we need to diversify our heuristics to include other notions of human flourishing. He leaves the content of those heuristics open. The most concrete existing answer in this vault is Qureshi's moral portfolio in [[nabeel-qureshi-principles]]: roughly four-fifths utilitarian, with deontology and virtue ethics as explicit minority holdings. That is a portfolio rather than a theory, which is arguably Smith's point.

Two observations Smith does not make. First, economics officially abandoned interpersonal utility comparison in the 1930s, after Lionel Robbins's critique, and retreated to ordinal preferences and Pareto efficiency, which permit no claim that Musk's loss is outweighed by strangers' gains. The redistribution intuition Smith opens with requires exactly the cardinal comparison his incommensurability section says is unavailable, so the discipline's own history already contains his argument. Second, the essay's structure is itself an instance of [[tradeoffs]]: every alternative heuristic he might add, from rights to virtue to sanctity of life, buys robustness against one class of monster by giving up the clean aggregability that made utilitarianism useful for policy in the first place.

## Sources

- Smith, Noah (2026-09-22). "The problem(s) with utilitarianism." *Noahpinion.* <https://www.noahpinion.blog/p/the-problems-with-utilitarianism> — [[2026-09-24-the-problems-with-utilitarianism|local copy]]
