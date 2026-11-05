---
source: agent
compiled_from:
  - agent-notes/raw/business/entrepreneurship/2026-11-04-how-to-talk-to-users.md
  - agent-notes/raw/business/entrepreneurship/2026-11-04-collect-stories-not-generalizations.md
compiled_at: 2026-11-04
model: claude-fable-5-1
confidence: medium
---

# Customer Interviews

**Customer interviews** — YC's phrase is "talking to users" — are the founder-run conversations that turn a hunch about a problem into hard facts about how specific people actually experience it. Eric Migicovsky (Pebble founder, YC partner) gave the canonical Startup School treatment in 2019, and is explicit that most of it is a synthesis of Rob Fitzpatrick's *The Mom Test* (2013). His framing: YC's teaching reduces to two activities, write code and talk to users, and the second is the one founders systematically outsource or do badly. The lecture supplies three things: the errors to avoid, five questions that work at any stage, and a different *purpose* for interviewing at each of the three pre-product-market-fit stages (idea, prototype, launched). Allen Pike's 2023 essay on **story orientation** tightens the second error: a problem-side question that asks people to generalize about themselves fails almost as badly as a hypothetical, and the repair is to ask for one recent episode.

## Founders do this themselves

Migicovsky's opening claim is organizational, not tactical: the best companies are the ones where the founders keep a direct line to users for the company's whole life. Hiring salespeople or heads of product does not discharge the obligation — "if you are the CEO it is in your job description." The engineer-founder is not exempt either; he invokes the *Office Space* go-between ("I have people skills!") as the role you must never need to hire. The implicit argument is about information loss: an interview's value lies in specific, unprocessed detail (who, when, which class, which file), and every hand-off between the person who heard it and the person deciding what to build strips some of that detail away. This is the same reason [[early-stage-startup-execution]] insists the founder makes the cold calls, and why [[design-partners]] treats early users as research subjects the founder studies personally.

## The three Mom Test errors

Fitzpatrick's title names the failure: pitching your idea to someone who loves you and wants to support you, then mistaking their encouragement for data. Migicovsky distils the book to three mistakes founders "pretty much all" make:

1. **Talking about your idea instead of their life.** An interview is for extracting information, not selling. The goal is specifics about the problem area as the user lives it, including the path that led them to the problem and their motivations for being there at all.
2. **Talking about hypotheticals instead of specifics.** "If we built this feature, would you use it / pay for it?" is the canonical wrong question. Ask about things that have already happened; past behavior is evidence, imagined future behavior is not.
3. **Talking instead of listening.** Founders spend all day pitching investors, hires, and partners, and the habit leaks. In a 10–30 minute interview the job is to take notes and come back to the co-founders with facts about users' lives, not a feeling.

## Five questions that work at every stage

Migicovsky ties each question to what it extracts, illustrated throughout with a hypothetical Drew Houston in the MIT computer lab in 2005 asking a classmate about group projects.

| Question | What it extracts |
|---|---|
| **What is the hardest part about [doing this thing]?** | Whether the problem is real and frequent enough to warrant solving. Open-ended; starts the conversation on their workflow (shared machines, network drives, two people editing the same file). |
| **Tell me about the last time you encountered this problem.** | Context: when, with whom, on what. Concrete episodes you can later overlay your solution onto to check it would actually have helped. |
| **Why was this hard?** | Different people name different pains (duplicated work from emailed copies; submitting the wrong version because of filename suffixes). These answers become positioning and sales copy — "customers don't buy the what, they buy the why." |
| **What, if anything, have you done to solve this?** | Two things: whether the pain is burning enough that they are *already* seeking a fix, and what your competitive set really is (the "just use rsync over SFTP" Hacker News commenter on Dropbox's launch counts). If nobody has tried anything, your better solution may be for a problem nobody feels. |
| **What don't you love about the solutions you've tried?** | The beginning of your feature set, derived from specific complaints about existing tools. Explicitly *not* "what features would you want" — users are poor at naming the next feature (Ford's faster horse) and excellent at describing what annoys them today. |

The sequence has a shape: question 1 validates the pain, 2 and 3 pin it to real episodes and real language, 4 tests intensity and maps competitors, 5 turns complaints into a roadmap. Question 3's output is what [[early-stage-startup-execution]] calls "the language prospects use becomes your landing page copy," and what [[consultative-selling]] and [[cold-outbound]] describe as quoting the buyer's words back to them.

## Stories, not generalizations

Allen Pike (2023) argues that moving from solution questions to problem-space questions is necessary but not sufficient. "How often do you struggle with X?", "What do you take into account when choosing Y?" and "Why don't you use approach Z?" pitch nothing and imagine no future, and by his account they still tend to produce untrue answers. Each one asks the interviewee to summarize their own behavior. His fix, taken from Teresa Torres's *Continuous Discovery Habits* (2021), is **story orientation**: ask for one recent, specific episode instead.

Torres's example, which Pike quotes in full, is a workshop attendee asked what she considers when buying jeans. "Fit is my number-one factor." Asked about the last pair she bought: on Amazon, with no way of knowing whether they would fit, because "they were a brand I liked, and they were on sale." The first answer is how she thinks she buys jeans. The second is how she bought them, and it names brand, convenience and price.

Pike gives the mechanism in two parts:

- **Compounding.** A story still carries memory errors. A generalization compounds them, because the person has to take every error-prone memory of X and compress the lot into one lossy summary.
- **Self-image.** The summary passes through the question *am I the kind of person who should struggle with X?* People "feel much more self-aware than they are." Nobody is lying, and neither side notices, which is why a friendly and cooperative interview offers no protection.

His own case was a round of interviews with leaders about time and attention. "How often do you spend time on things that are urgent but not important?" returned accounts of disciplined focus and almost no pain points, since competent leaders see themselves as people who work on what matters. He rewrote the questions, and the three rewrites show three distinct patterns (the labels are this article's reading, not Pike's):

| Reworked question | Pattern |
|---|---|
| "Can you tell me about a time recently when you dropped a ball?" | Ask for the episode directly, and name the failure so the interviewee does not have to volunteer it. |
| "You described planning every week the Friday before. Tell me about how you planned out this week, and how that went." | Take a habit they have just claimed and ask for this week's instance of it. |
| "About how many Slack notifications did you defer from yesterday to today?" | Replace "how often" with a count over a short, fixed, recent window. |

Interviewees who had just explained how rigorously they manage their time would "backpedal and rethink their answers" once asked for specifics.

Pike points out that hiring made the same move when "How do you approach conflict in the workplace?" gave way to "Tell me about a time you had conflict in the workplace," and that journalism and social science rely on it for the same reason. Within this wiki, the two questions in [[hiring-for-curiosity]] test "behavior, not stated values," and [[founder-evaluation]] records Rabois's view that grit shows up in anecdotes the founder does not know are revealing. The self-image filter is what [[psychology-of-human-misjudgment]] lists as Excessive Self-Regard. Pike cites no research beyond Wikipedia's entries on false memory and confabulation; the standard reference is Nisbett and Wilson's "Telling More Than We Can Know" (1977), which found that people explaining their own behavior often report a plausible theory rather than anything they observed in themselves.

What this changes in the rest of this article:

- **The five questions are not equally trustworthy.** Question 1 ("what is the hardest part?") is a generalization by Pike's standard; question 2 ("tell me about the last time") is the story. Treat the first answer as the interviewee's theory of their own problem and the second as the evidence. When they disagree, as with the jeans, the episode wins.
- **The prototype-stage numbers need the same repair.** "How frequently do you hit this?" and "what does it cost you?" invite summaries. Pike's Slack question is the template: how many times last week, and what did the most recent one cost.
- **Fitzpatrick already had the category.** *The Mom Test* files generic claims ("I usually," "I always," "I never") under fluff, next to future-tense promises and hypothetical maybes. Migicovsky's lecture compresses that into one line about discarding fluff at the launched stage. Pike's contribution is to make it the organizing rule for every stage and to say why it happens.
- **The gap between the two answers is data.** Pike's caveat is that the self-deception still matters for marketing: a problem people do not know they have is harder to sell a fix for. The generalization is the self-image the copy has to speak to; the story is the behavior the product has to serve. A jeans retailer would advertise fit and compete on brand and price.
- **One story is one data point.** A recent episode can be unrepresentative, and Pike concedes stories carry their own memory errors. Story orientation does not remove the need to generalize; it moves the generalizing from the interviewee, who does it badly about themselves, to the interviewer, who does it across many episodes and many people. Pike's closing test is the practical check: reread the notes and count how many lines are stories.

## Idea stage: find the first people with the problem

Before any product exists the aim is simply to find people who have the problem and will describe it.

- **Start with yourself.** Many of the best products are built for the founder; run the interview on your own last encounter with the problem first.
- **Then friends and coworkers, by warm intro.** A research program begins with one or two people, not thousands; what matters is that the interview is unbiased and detailed, not that it is numerous.
- **Just show up.** A YC company selling to firefighters got nowhere with cold email, so they walked into fire stations unannounced, asked for the chief, and got dozens of 10–15 minute meetings. Migicovsky's reframe for the discomfort: if you genuinely think you are solving their problem, taking fifteen minutes of their day is a favor to them.
- **Industry events, guerrilla-style.** Pebble went to CES with no booth and no budget and set up meetings in the conference coffee shop, because the people they needed were concentrated there.

Tips for the stage: take detailed notes (you will not know until later which fact mattered), bring a co-founder or ask to record, keep it casual rather than calendar-blocked, expect the first five or ten interviews to change your process dramatically, and respect the other person's time — a first interview of 10–15 minutes is usually enough.

## Prototype stage: identify the best first customer

Once there is something to show, the purpose of interviews shifts to choosing *whom to build for first*, because Migicovsky argues the wrong first customer can constrain you or trap you without ever paying. He asks for **numerical answers to three facts**:

1. **How much does the problem cost them today?** A hard number — revenue they would gain, or expense currently wasted, by solving it.
2. **How frequently do they encounter it?** Hourly, daily, quarterly, yearly. Frequent problems win twice: the customer feels the pain more often and is more receptive, and you get more cycles to learn whether the product is working. Pebble's daily-wear habit was his own leading indicator — a watch left in the drawer meant something was wrong.
3. **How large is their budget, and do they have the authority to spend it?** The assembly-line operator feels the problem hourly but cannot buy the fix; their boss in headquarters can.

Picture the three as overlapping circles with the best first customer at the center. His worked example is a smart blender pitched to the French Laundry (high value per sale, low frequency, a sous-chef with no budget), a Google café (high volume but the food is free, so no revenue motive and no budget), and McDonald's (low value per transaction, enormous frequency across thousands of stores, and a warm intro to someone controlling a multi-billion-dollar budget). Put the answers in a three-column spreadsheet and stack rank.

This maps almost exactly onto the Amble/Li screen in [[design-partners]]: frequency is their *urgency*, budget-plus-authority is their *capacity*, and cost-today is what makes a partner representative of a paying market rather than a curiosity. The operator-versus-boss warning is the mirror image of their "CEOs are a capacity trap" — in both cases the lesson is to interview the person who can both feel the problem and fund the solution, and to notice when those are two different people. It is also the concrete version of the problem-discovery lens in [[product-management-framework]]: go deep with interviews, but score what comes back.

## Launched stage: a leading indicator for product-market fit

Migicovsky's complaint about the standard PMF definitions — Graham's "something people want," Andreessen's "the product is being pulled out of you" — is that they are vague and retroactive: you have to already have PMF to know you have it, so they cannot guide the next week's work. He points to Rahul Vohra's account of building Superhuman's "product-market fit engine" (First Round Review, 2018; see [[product-market-fit]]) as the fix: ask a sample of users (30–40 is enough) every week, *how would you feel if you could no longer use the product?* — very disappointed, somewhat disappointed, not disappointed — and track the share answering *very disappointed*. Those are the users for whom the product has become habit. The threshold Vohra adopted is 40%: companies at or above it tended to grow on their own, and the weekly measurement tells you whether last week's features moved the number. (The talk credits "some analysis" for the threshold; it originates with Sean Ellis's growth surveys.)

Three tactical tips for this stage:

- **Ask for a phone number high in the signup flow.** When the aggregate data says 20% of users hit some problem, the fastest way to understand it is to call one of them.
- **Don't design by committee.** Instead of "would you use this feature?", put an upgrade flow in front of them that asks for a credit card *before* the feature is built. Payment intent is the only hypothetical worth collecting.
- **Discard bad data.** Compliments ("I love the new design") are not specific or actionable. Fluff — hypotheticals and generic statements about what the product could become — should be steered back to specific past episodes.

## Assessment

The lecture is a compression of *The Mom Test* with YC war stories layered on, and it inherits the book's strengths and one of its gaps.

- **Strength: it is entirely problem-side.** Every question asks about the past and about pain; none pitches. That discipline is what makes the output usable as evidence rather than encouragement, and it is why the five questions survive contact with any industry.
- **Gap: commitment.** Fitzpatrick's book spends a chapter on asking for *commitment and advancement* (time, reputation, money) as the antidote to compliments. The talk reaches for this only at the launched stage with the credit-card test; at the idea and prototype stages it leaves "would they pay?" implicit in the cost and budget numbers. [[startup-ideation-framework]] fills the hole bluntly with its ten-paying-customers test, and [[design-partners]] deliberately excludes willingness-to-pay from selection and reintroduces it at conversion — a sequencing Migicovsky's three-stage model would agree with but does not state.
- **Caveat on question 4.** "Nobody is already trying to solve it" is a strong filter against problems people do not feel, and usually correct. It can also screen out categories users have resigned themselves to; the honest reading of the Dropbox example is that the people hacking rsync were the signal of latent demand, not the market. Treat an empty answer as a flag to probe harder on frequency and cost, not as an automatic kill.
- **The frequency point does double duty.** Migicovsky's second reason to prefer frequent problems — more learning cycles — is underappreciated relative to the first. It is an argument about the founder's *information* rate, not the customer's pain, and it connects to the search-not-execution framing in [[minimum-viable-product]] and [[commit-and-go-deep]]: a daily-use product tells you every day whether you are wrong.
- **Pebble is the cautionary footnote to its own example.** It passed the frequency test (worn daily), shipped roughly two million watches, and still ran out of cash in 2016 and sold its assets to Fitbit. Interviewing well tells you the problem is real and who to build for first; it does not protect the business model.

## Sources
- Migicovsky, Eric (2019). "How to Talk to Users." Y Combinator Startup School. <https://www.youtube.com/watch?v=MT4Ig2uqjTc> — [[2026-11-04-how-to-talk-to-users|local copy]]
- Pike, Allen (2023). "Collect Stories, Not Generalizations." <https://allenpike.com/2023/stories-generalizations-product-interviewing/> — [[2026-11-04-collect-stories-not-generalizations|local copy]]
