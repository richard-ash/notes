---
source: agent
compiled_from:
  - agent-notes/raw/psychology/2026-06-30-be-impatient.md
compiled_at: 2026-06-30
model: claude-opus-4-8[1m]
confidence: medium
---

# Speed compounds

Ben Kuhn argues that **impatience is a productive disposition**: the habit of constantly asking "how could this take less calendar time" makes you faster at things, and across a surprising number of domains, being fast correlates strongly with being effective. The essay's framing device is Kuhn admitting to running a mental [critical-path analysis](https://en.wikipedia.org/wiki/Critical_path_method) on any everyday activity longer than 15 seconds — the trait is real, the airport-abandonment manifestation is the part not to copy.

## The convergence of datapoints

Kuhn concedes most of these are non-causal correlations; the argument is the *number* of independent domains where speed predicts effectiveness:

- **Email** — Sriram Krishnan and Sam Altman both observe that famous, powerful, busy people answer their own email quickly; Altman has "almost never made money investing in founders who do not respond quickly to important emails." Fast-mover vs. slow-mover is treated as a stable, hard-to-change personal type.
- **Startups** — Altman's claim that the single best YC predictor of success is *whether a team has gotten new things done every time you talk to them*. Bias toward action over grand plans. Propagates down to deploy cadence: Instagram's continuous deployment ("Yolout"), and *Accelerate*'s finding that high performers deploy 46× more often with 440× faster lead time.
- **Apps/tools** — speed matters even where things are already fast. Google's page-load data (BBC lost 10% of users per added second; 53% of mobile visits abandoned past 3s). James Somers on Google search making search feel like "an extension of your own mind" because there's no delay between thought and action.
- **Personal workflow** — typing speed and keyboard shortcuts among the best engineers (Altman, Yegge); Kuhn corroborates from Wave.
- **Negotiations** — moving candidates through hiring faster raises offer-acceptance (Wave); "time kills all deals" in sales; the Collison brothers' "give me your laptop" on-the-spot install; Fred Wilson's "go to lunch tomorrow, he won't remember you next month."
- **Combat** — John Boyd's OODA loop: getting *inside* an adversary's observe-orient-decide-act cycle is decisive; the same lens applied to COVID, where the virus got inside governments' OODA loops.
- **Life in general** — Patrick Collison and Altman on doing great things young and accomplishing priorities quickly.

## The load-bearing mechanism

The naive case for speed is linear: 10% more productive → 10% more total output. Kuhn says that's *not* the main reason. The quotes are all about **processing information faster**, not churning out more work — and the faster you process information, the faster you fold the result into your next move.

So the real benefit is that **you end up doing different things**, not the same things faster. This is Nelson Elhage's observation generalized: *faster tools change how the tool is used.* Sorbet became developers' first feedback line at Stripe purely because it was the fastest option; livegrep gets used *interactively* — query, read results, refine — in a way slow search engines never are. Mediocre feedback now beats good feedback in minutes.

The consequences are kind: respond to email fast and you surface opportunities you'd otherwise never see and reprioritize toward them; make tests 10× faster and you can switch to [test-driven development](https://en.wikipedia.org/wiki/Test-driven_development) and catch mistakes before going down bad paths; ship a week earlier and you get a week's head start on real user feedback.

This is why speed **compounds** rather than adding: being twice as fast doesn't just double output, it doubles the *growth rate* of output, because each cycle's learning feeds the next. Over time the gap is enormous. The mechanism is the same iterated-feedback loop Boyd described for combat — a tighter OODA loop wins not because each action is better but because you take more of them per unit of the opponent's time.

## Connections

- The "every time we talk to them they've gotten new things done" predictor is the velocity face of [[wiki/business/entrepreneurship/founder-evaluation|founder evaluation]] — Graham's "relentlessly resourceful," Altman's fast-mover type, and Rabois's bias-to-action all point at the same trait that this essay isolates as *speed of iteration*.
- Kuhn's claim that the gain is in *processing information* faster — not doing more work — is a useful counterweight to productivity systems that optimize throughput of a fixed task list; see [[personal-productivity-systems]]. Speed's value is changing *which* tasks you do, not finishing the same ones sooner.
- The OODA-loop framing — win by iterating faster, not by being individually smarter on any one move — rhymes with [[shut-up-and-do-the-impossible]]'s emphasis on extraordinary effort over any single clever insight, and with [[dialogic-thinking]]'s split between understanding (cheap to iterate, social) and committed action (solitary): faster loops are most valuable in the iterate-to-understand phase.

## Caveats

Kuhn flags two himself. First, almost all the evidence is correlational — fast movers may simply be more capable people, with speed a symptom rather than a cause. Second, the disposition has an antisocial failure mode (the Ethiopian-airport story); the recommended part is the internal habit of minimizing calendar time, not externalizing impatience onto the people around you. Worth adding: the essay's domains all reward iteration speed because feedback is cheap and reversible. Where a decision is high-stakes and irreversible, the OODA loop runs only once and the compounding logic doesn't apply — speed there buys nothing and can cost everything.

## Sources
- Kuhn, Ben (2020-07-23). "Be impatient." <https://www.benkuhn.net/impatient/> — [[2026-06-30-be-impatient|local copy]]
