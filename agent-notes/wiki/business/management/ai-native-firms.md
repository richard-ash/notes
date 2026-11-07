---
source: agent
compiled_from:
  - agent-notes/raw/business/management/2026-11-07-ai-native-firms.md
compiled_at: 2026-11-07
model: claude-opus-5-5
confidence: medium
---

# AI-native firms

"AI-native" gets used for two different things: a firm whose people work through AI tools, and a firm whose product does work with AI. Hyunjin Kim (INSEAD) and Rembrand Koning (HBS) separate the two in *AI-Native Firms* (SSRN, June 2026) and measure how each relates to firm shape. Their sample is Y Combinator batches W20–F24 plus U.S. venture-backed startups whose first financing closed in 2020–2024, linked to Revelio Labs workforce data. Compared with non-AI startups in the same industry and cohort, AI-native startups are about 25% smaller, more technical, more senior and flatter, and they carry similar valuations. Most of the gap lines up with AI built into the product, not with workers using AI tools. It is biggest where the pre-AI business grew by hiring people to deliver a service.

## Process channel and product channel

- **Process channel.** AI changes how employees code, sell, design and coordinate. Most recent research studies this channel through task-level experiments (Copilot, customer-service assistants, consulting tasks).
- **Product channel.** AI is part of what the firm sells, so the product performs knowledge work that would otherwise need a human team, at the firm or at its customer.

The authors build the argument on the information-processing view of the firm (Simon, March & Simon, Galbraith, Garicano): routines and hierarchy exist so that people can process information and coordinate, which ties growth to hiring. Ide and Talamás (2025) model autonomous AI as making noncodifiable expertise scale through compute. Kim and Koning take the next step. Even autonomous AI deployed *inside* production leaves the firm managing a workflow for every unit of output: scope the request, coordinate the work, deliver it. When the AI sits *in the product*, the customer specifies, evaluates and iterates in the interface, and output scales with compute. They predict three effects: less labor per unit of output, flatter structures (requests go through the product instead of up a knowledge hierarchy), and higher technical density (staff build the product instead of doing routine production).

Two case studies illustrate this. **Gamma** (AI presentations) can be read as millions of semi-autonomous agents, each making one deck for one user. Around 30 employees served millions of users and reached $50M in annual revenue in two years. A traditional presentation-services firm that used AI internally would still turn each deck into a staffed workflow. **FazeShift** automates accounts receivable end to end (invoicing, collections, cash application, discrepancy resolution) with ten people across dozens of enterprise customers. A conventional AR SaaS vendor would need far more staff both to build the exception handling and to resolve the exceptions. The authors note one counterforce: if AI makes the product much cheaper, Jevons-style demand growth could mean more hiring, not less.

## Data and design

- **YC sample:** 2,891 startups across 11 batches. A firm counts as AI if it tagged itself "artificial-intelligence" or "ai" on its YC profile: 990 firms (34.2%). The AI share of YC batches rose from about 15% in early 2020 to over 50% in 2024. 96.4% matched to PitchBook and 77.2% to Revelio (January 2025 snapshot). Firms with no Revelio match are coded as zero employees, and results hold when they are dropped instead.
- **PitchBook sample:** U.S. startups with a first financing deal in 2020–2024. AI status is predicted from company descriptions: text-embedding-3-large embeddings feed a random forest trained on the YC tags (CV AUC 0.81, precision 74%, recall 55%). The predicted AI share grew from about 8% to over 20%.
- **Design:** descriptive cross-sections with batch × industry (or first-deal-quarter × industry) fixed effects, so AI firms are compared with non-AI firms that entered the same industry at the same time. The authors deliberately exclude the between-industry effect, where AI pulls firms into industries with different team structures. That makes the estimates conservative. By Chandler's logic, choosing a different industry is itself one way a technology reshapes firms.

## What they look like

Raw YC means: 13 vs 42 employees, 3.8 vs 5.0 seniority levels, 17% vs 24% managers, 45% vs 36% engineers, 19% vs 30% entry-level. Within industry-cohort cells:

| Outcome | YC | PitchBook |
|---|---|---|
| Headcount, levels | −8 (non-AI mean 34) | −6 (non-AI mean 18) |
| Headcount, log (firms with ≥1 employee) | ~−25% | ~−12% |
| Engineering share | +4.5 pp | +18 pp |
| Entry-level share | −4 pp (~15% relative) | −6 pp |
| Senior share | +5 pp | +6 pp |
| Hierarchy depth | −0.48 levels (holds controlling for size) | — |
| Manager share | −3.7 pp (~15% relative) | — |
| Total funding | ~−15% | ~+15% (p < 0.10) |
| Valuation | n.s. | +58% |
| Funding per employee | +12% (p < 0.10) | +33% |
| Valuation per employee | +30% | +76% |

- Sales, finance, operations and admin shares are all lower, so the cut covers both external-facing and internal-process functions. Because the firms are smaller overall, AI-native firms have fewer people in every function, engineering included in absolute terms.
- The size gap is not just a cohort effect. Measured in quarters since YC graduation, AI firms are about half the size of non-AI firms, and the gap holds for at least three years.
- Valuation per employee rises more than funding per employee. The authors read this as investors expecting higher productivity per unit of capital and labor. It is a market-implied productivity measure, not realized output.
- The labor pool is narrower. AI startups are 20 pp more likely to be headquartered in San Francisco, and their employees are more likely to hold graduate degrees (+5 pp in YC, +17.6 pp in PitchBook). In PitchBook the female share is 5.9 pp lower and the prestige of employees' universities is higher.

**Level-of-analysis inversion.** Task-level studies keep finding that AI helps less-experienced workers most. At the firm level, AI-native firms hire *fewer* juniors and *more* seniors. The authors' point is that who gains from AI depends on where it enters production, not only on task-level productivity. The firm-level result matches Brynjolfsson, Chandar and Chen's 13% relative drop in early-career employment in AI-exposed occupations.

## The product channel does most of the work

**Measuring the product channel.** The authors read 40 AI-tagged YC descriptions, derived a four-way schema, and had an LLM apply it to all 990 AI-tagged firms:

| Category | Share | Examples |
|---|---|---|
| Autonomous workflow (AI does work people used to do) | 43% | Artisan (AI SDRs), Aurelian (AI 911 triage) |
| Expert augmentation (AI extends a professional's workflow) | 24% | Tower (legal), Medium Biosciences (protein design) |
| AI infrastructure (others build on it) | 15% | Exa (neural search), Roboflow (vision) |
| Other / unclear | 18% | games, robotics |

About two-thirds clearly build AI into what they sell. The same schema was applied to non-AI firms so the regressions code both groups the same way.

**Measuring the process channel.** A firm counts as process-channel if any of its own job postings names one of 33 specific tools (ChatGPT, Claude, Copilot, Cursor, V0, Midjourney, Granola, …). Postings that only describe AI features being built do not count. Among the 1,666 firms with postings and employees, 69.8% of AI-tagged firms show the product channel vs 16.1% of non-AI firms. For the process channel the figures are 13.5% vs 5.2%, a 2.6× gap but a much smaller absolute level.

**Results.** Both measures go into the same regression. The product channel predicts about 10 fewer employees, about 13% smaller on the log margin, 19% smaller in Poisson, and about 0.2 fewer layers. The process channel predicts nothing significant on log, Poisson, hierarchy or manager share, and its levels coefficient is *positive* (+45, p < 0.10). The authors call the process proxy "coarse and noisy," since job postings understate tool use, and they do not claim that tools have no effect.

The null result fits the "mapping problem" from Kim, Kim and Koning's 2026 field experiment: access to AI is not what limits adoption. The limit is finding where in the firm's own processes AI creates value. Firms that solve this grow faster with less capital and no added labor. Read that way, handing workers Cursor does not by itself make a firm smaller. Re-engineering the process does, and so does moving the process into the product.

## Services shrink the most

If AI in the product replaces delivery labor, the largest gaps should appear in businesses that used to grow by adding worker-hours. Nearest-neighbor pairs on description embeddings show the extremes:

- Educato AI (AI exam prep): 7 employees. Careerist (courses taught by third-party tutors): 912.
- Legion Health (AI psychiatry built on LLMs and agents): 28. Intellect (mental health through a network of human therapists): 446.

Systematically: in software, the reference category, AI startups are about 25% smaller (β = −0.286). In services-delivery industries (healthcare services, commercial services, media), the interaction adds another −0.929 log points, which puts AI startups at about 30% of their non-AI peers' headcount. Hierarchy is 0.375 levels flatter in software and another 0.45 flatter in services. The "other" bucket (biotech, hardware, fintech, devices) shows no extra effect.

This is [[task-automation-vs-paradigm-replacement]] in firm form. A tutoring marketplace that gives its tutors AI tools is task automation inside the old model. An exam-prep product where the AI is the tutor replaces the model, and the paired headcounts differ by 16× to 130×, not 25%.

## Implications

- **Capability moves out of the org chart.** The authors' broadest claim: if firms can import capabilities from foundation models instead of building them through people, human attention stops being the constraint on scale. The management problem then shifts from accumulating internal capacity to integrating outside capabilities into products. Competitive advantage may come from building, importing and orchestrating model capabilities as much as human ones. That moves the Teece/Helfat dynamic-capabilities question onto the model supply chain, which ties into [[ai-value-capture]] (who captures the rent when the capability is rented).
- **A different mechanism from the coordination story.** [[ai-and-the-theory-of-the-firm]] (Imas, Koh and Legg) cites these numbers (25% smaller, about 15% fewer juniors and managers) as evidence for its "composition change, not scale change" regime, where competent AI with weak coordination makes firms leaner and flatter. Kim and Koning's mechanism is different. In the product channel nobody inside the firm coordinates the work, AI or human. The customer specifies and judges the output in the interface, so the work leaves the firm instead of being reorganized within it. That is a firm-boundary effect, not a change to the model's internal coordination parameter. The two accounts make different predictions. The coordination story says firms will grow again if AI teams ever coordinate better. The product story says the gap will last wherever the customer can do the steering.
- **The process is the unit, and here it moved.** Bret Taylor's [[ai-and-org-design]] argues that the process, not the person, is the atomic unit of AI productivity, and that departmental seams block the payoff. The FazeShift and Gamma cases take that one step further: the whole process is packaged and runs in the customer's hands, so the seams never have to be staffed.
- **Where the playbooks put their weight.** [[ai-native-company-building]] (Hu, Rabois) is mostly about the process channel: the company runs on AI, the loops are closed, the work happens in software factories. This paper's evidence, with its weak process proxy kept in mind, suggests most of the measurable headcount gap comes from *what* AI-native firms build, not *how* they run. The two are complements, and a founder copying the operating model without the product architecture should not expect the size difference.
- **Per-firm shrinkage is not aggregate labor demand.** AI firms are about half the size of their peers after three years, so entry would need to roughly double to offset the gap. In PitchBook, AI first deals in 2024 were nearly 8× the 2020 average. Some of that entry displaces non-AI ventures, and the authors leave the net effect open. [[solopreneur-economy]] supplies the matching entry-side evidence (more and richer nonemployer firms), and [[messy-jobs]] shows why task-exposure measures miss firm-level reorganization. This paper measures use (tags, product design, named tools) rather than exposure.

## Limits

The authors list most of these themselves:

- **Self-identification.** An "AI" tag could be strategic, as with adding ".com" to a name in 1999. The authors argue a symbolic label would move valuations, not the third-party LinkedIn org structures they measure.
- **Cross-section, not cause.** The design cannot separate product architecture from internal efficiency or from *founder selection*. The narrower, more credentialed, more male, more SF-based workforce is just as consistent with different people starting AI firms.
- **Few years of data.** Whether coordination demands return as these firms scale is unknown.
- **Inferred AI status in PitchBook.** With 55% recall, the authors warn this "may mechanically inflate compositional differences," which may be why the PitchBook engineering-share coefficient (+18 pp) is four times the YC one.
- **Measurement sources.** Headcount comes from LinkedIn-derived Revelio records, and valuations are expectations. Gamma, FazeShift, Educato and Legion are hand-picked illustrations, not the estimate.

## Sources

- Kim, Hyunjin and Rembrand Koning (2026). "AI-Native Firms." SSRN working paper 6905079. <https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6905079> — [[2026-11-07-ai-native-firms|local copy]]
