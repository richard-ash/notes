---
source: agent
compiled_from:
  - agent-notes/raw/business/marketing/2026-09-12-yc-zero-replies-cold-emails.md
compiled_at: 2026-10-02
model: claude-fable-5-1
confidence: medium
---

# Cold Outbound

**Cold outbound** is unsolicited sales outreach, by email or LinkedIn, to people
who have never heard of you. This article covers the founder-led, pre-scale
version: the first few hundred messages a founder sends before there is a sales
team, a sequence tool, or a proven pitch. Its spine is Christina Gilbert's
eight-tip YC talk (2026). Gilbert founded OneSchema, where she says she
personally generated and closed millions in revenue, and as a YC Visiting
Partner she reviews founders' outbound in office hours. Her claims are
practitioner heuristics drawn from that experience; she cites no data.

The unifying idea is that early outbound is a **learning instrument before it
is a revenue channel**. Every tip either makes the experiment interpretable or
feeds what it teaches back into the next message.

## Manual before automated

The failure Gilbert sees most often: a founder loads a tool, blasts a thousand
emails, and gets zero replies. The cost is not the wasted sends but the wasted
experiment. Zero replies from an unconsidered campaign teaches nothing, because
five variables are confounded: messaging, company targeting, prospect selection,
deliverability, and subject line.

Her prescription is **at least 100 outreaches genuinely by hand** ("honestly
probably going to end up being more"): think about one person, her specific
problem, what would capture her attention; read her LinkedIn and her company's
site. The homework is where the highest-converting ideas come from.

This is the email form of two ideas already in the vault. The founder in
[[early-stage-startup-execution]] reframes cold calling from selling to
learning, and Cheng in [[consultative-selling]] defines marketing as "sales in
print" and holds that you cannot reliably sell one-to-many what you have never
sold one-to-one. Automation scales a message; it cannot find one.

## Targeting beats messaging

Gilbert argues founders spend hours on copy and almost no thought on the
recipient, when the recipient matters more: "those wrong job titles were never
going to buy, no matter how good your email was." Her example is a winter-batch
infrastructure startup that should have been selling to senior engineering
leaders and was instead messaging DevRel managers, GTM managers, and a customer
success manager, hundreds of times.

**The right person.**
- With customers: look at the last deals. Who pushed it to close, who signed,
  who paid? Target people with those titles, plus the titles of anyone who has
  already replied.
- Without customers: ask who in the organization has the most to gain. For
  employee-device security monitoring, a chief security officer can be fired
  over a breach; an engineering manager would rather not be monitored at all.

**The right company.** List-building tools return near-misses. Searching "tech
companies" in LinkedIn Sales Navigator yields a pile of IT implementation
consultancies. Gilbert's rule is to verify each company individually.

**Intent signals.** Observable clues that a company needs the product now. Job
postings reveal priorities. Company growth is another: compensation-planning
software is useless below about 100 employees (no levels yet) and late above
500 (bands already set), so crossing the 100-employee range is the signal.
"Every product has signals like this. Your job is to discover yours."

**Warm network first.** For the very first customers, "shake the tree":
friends, family, investors, the college roommate, "a guy you met at a cafe."
Conversion is much higher than cold.

Gilbert's ordering is the same claim as Cheng's
[[strategy-to-sales-call-hierarchy]]: "a superior sales call cannot compensate
for poor market strategy." Intent signals are his second tier (fit *and*
timing; his own example is the cyber-security consultant calling the day after
a breach lands on CNN), and they are the outbound counterpart of the urgency
screen in [[design-partners]]. The who-signed-who-paid test also guards against
that article's CEO capacity trap: target the person with the problem and the
authority, not the most senior name you can find. Where signer, payer, and
champion turn out to be different people, [[multi-stakeholder-selling]] takes
over.

## Anatomy of the message

| Element | Gilbert's rule |
|---|---|
| Problem | A crisp statement of how you can help *this* person. Work from the top three things that keep the buyer up at night: what gets them fired, what gets them promoted. |
| Product | One sentence. Details are what the first call is for. Executives "don't care that your database is built in Rust"; they care about the quarterly target. |
| Credibility | Names of impressive companies you already help, or, lacking those, your directly relevant background. |
| Call to action | Specific and easy to answer: "Got 20 minutes to hop on a call this week?" rather than "Does this sound interesting to you?" Add a calendar link or a few time slots. |
| Length | Five to eight sentences for email, two to five for LinkedIn. "Every filler word that you use dilutes the ones that matter." |

The mechanism she relies on is problem recognition: when the buyer thinks
"that's exactly the problem I have, they really get it," they take the call
"even without fully understanding or trusting your solution." That is the
Problem step of Cheng's PCNS compressed into a few sentences; the email has to
earn the conversation in which the rest of [[consultative-selling]] happens.

**Worked example.** Gilbert holds up an email from a YC S24 founder (the
auto-transcript garbles the company name as "Aptton"). It opens: "I used to be
a software engineer at Tesla. We got crazy good at using SMS to convert the
people who visited our website into car buyers." It notes that the recipient's
site collects phone numbers at signup, and closes: "Would you be open to an
experiment to see if we could improve your conversion rate by using AI to
reactivate leads?" What she praises:
- An informal, jargon-free tone that reads like a peer, "an email that could
  have come from his friend."
- Credibility from having solved the same problem at a reputable company.
- Personalization grounded in something he actually observed.
- Almost no explanation of how the product works.

The convergence with [[asking-for-help]] is close. Prasad wants context "so
short as to be unsummarizable," and jackconsidine got zero replies from 100
laborious handwritten notes and 15% from short emails with a clear ask.
Gilbert's two credibility routes map onto Prasad's ladder (customer logos are
institutional credibility, relevant background is closer to proof of work); the
Tesla line works because it is both. The phone-number detail is the sales
version of lisper's "cite their own work," and it answers currymj's warning
that LLMs have made generic flattery cheap: only a specific, checkable
observation shows that a human looked.

## Gatekeepers: subject line and profile

The message is only read if something upstream earns the open.

- **Subject line and preview.** The subject plus the first 20 to 30 characters
  of the body (the Gmail preview) decide the open. Gilbert finds good ones by
  experiment, and "creative and kind of weird" often wins: for an agent
  product, "broken agents" clearly outperformed the more descriptive "better
  agents for every workflow."
- **LinkedIn profile.** "If email has subject lines, LinkedIn has your
  profile." Have a profile picture; turn the banner into a jargon-free ad for
  the company; rewrite the headline and About section as short descriptions of
  what the company does; cut hobbies and anything else a buyer would not care
  about.
- **Mutual connections.** Gilbert calls shared contacts the single biggest
  predictor of whether a connection request is accepted. People in the same
  customer profile know each other, so she recommends maxing out the daily
  connection allowance as a habit. This manufactures a weak form of the
  borrowed-connection credibility in [[asking-for-help]].

## Reading reply rates

Two or three replies per hundred emails is "a great place to start iterating":
a baseline exists. From there Gilbert debugs in a fixed order:

1. Right person
2. Right companies
3. Subject lines
4. Messaging
5. Materials (website, LinkedIn profile)
6. Deliverability

If all six look reasonable and replies are still zero, she reads it as a
possible product-market-fit problem rather than an outbound problem.

Messaging, where founders instinctively start, is fourth. The list is Cheng's
hierarchy laid out as a checklist: exhaust the strategy tiers before touching
the copy. The one surprise is deliverability in last place, since a message in
the spam folder makes the other five moot. A plausible reading (not stated in
the talk) is that the order assumes the manual regime she just prescribed:
low-volume sends from a real mailbox rarely trip spam filters, and a non-zero
reply rate already proves something is landing. For an automated campaign with
literally zero replies, checking deliverability earlier would be the cheaper
test.

## Follow up, break up, reply fast

- **Follow up two to four times**, a couple of days apart. One email is never
  enough because the likeliest explanation for silence is that it was missed.
- **End with a breakup message**: "Since I haven't heard back, it seems like
  sales tax automation isn't a priority for you right now, just let me know and
  I can spare your inbox." Gilbert finds reply rates much higher on these
  because a no has become cheap to give.
- **A real no is data.** "In aggregate, the many nos improve who you target in
  the future." The founder in [[early-stage-startup-execution]] says the same
  about cold calls: someone telling you exactly why they don't care beats
  someone nodding along.
- **Reply fast.** Once a prospect answers, be "a heat-seeking missile" for
  their calendar. "Time kills deals."

The breakup email is [[asking-for-help]]'s easy-to-say-no principle used as a
tactic. That article warns that granting permission to decline in the *first*
message shrinks the ask. Gilbert's placement avoids the problem: the release
comes only on the last touch, after the full-strength ask has been made
several times. Both sources bound the number of touches and then stop.

## Activity discipline

Gilbert calls not doing the outbound one of the biggest founder mistakes.
Outbound is among the least fun jobs a founder has, so anything else wins the
hour. Her fix is a concrete plan: messages per day, minutes per message, and a
calendar block for when they get sent, with a co-founder as backstop. "The
number one difference" between founders who succeed and those who don't, in
her telling, is following through on the activity they committed to. This is
[[schlep-blindness]] operating at the level of the daily calendar rather than
idea selection.

## Customer language and compounding

"The best feedback on your messaging always comes from your customer. Not a
friend, not an adviser, and not your co-founder." Two ways to collect it:

- Open the sales call with "What got your attention about my message?" The
  answer names the lines worth keeping and starts the buyer talking
  open-endedly about their problem.
- Ask existing customers the single thing that got them to buy, then reuse
  their phrasing. "Your customers are always going to write better copy than
  you do."

Cheng's version in [[consultative-selling]] is "I never use my own words to
convince a buyer. I quote their words back to them"; in
[[early-stage-startup-execution]] the language prospects use for their pain
becomes the landing-page copy. Gilbert closes the loop: the words that win one
buyer become the cold email to the next.

Her final argument is that the slog compounds and cannot be delegated. A
founder who has done the reps will "spot a job posting and instantly know that
that company has pain," and will know which pain point to lead with at which
company size. "No salesperson or agency will ever be able to learn about your
customers the way that you can." This is the go-to-market face of the depth bar
in [[commit-and-go-deep]], and the remedy for the founder pathology in
[[distribution-strategy]]: technically excellent teams assuming customers will
line up for a great product.

## Tensions and caveats

- **The exemplar bends the CTA rule.** Gilbert prescribes a time-boxed ask
  ("Got 20 minutes...?") over an interest check, but the email she praises
  closes with "Would you be open to an experiment...?", which is an interest
  check. What the two share is that each can be answered yes or no in one read;
  that, rather than the calendar request, seems to be the operative principle.
- **"Got 20 minutes" versus the labor-asymmetry objection.** Robay in
  [[networking-as-relationship-building]] treats "I'd love 15 minutes of your
  time" as a bad ask because it costs the sender seconds and the recipient half
  an hour. The sales version survives only when the preceding sentences have
  made the call worth something to the buyer. Without an accurate problem
  statement it is the same pick-your-brain request.
- **Reply rates are not comparable across kinds of ask.** Gilbert's 2 to 3
  percent baseline is for sales outreach; jackconsidine's 15 percent in
  [[asking-for-help]] was for requests for advice. Both point the same way on
  length.
- **The channel is credibility-light by construction.**
  [[credibility-based-selling]] describes sales as a byproduct of credibility
  built over years. Cold outbound is what a founder does before that exists,
  which is why Gilbert routes the first customers through the warm network and
  spends so much of the talk on borrowed proxies: logos, a past employer,
  mutual connections.
- **Scope.** The advice is drawn from B2B software companies in YC. The
  quantitative-sounding claims ("much higher," "single biggest predictor") are
  her observations, not measurements.
- **Timing.** The talk arrives when AI sequencing tools have made the
  thousand-email blast nearly free. That presumably raises the noise in every
  buyer's inbox and with it the value of the manual signal, which may be why
  manual-first is tip number one. This is an inference; Gilbert does not
  discuss AI tooling.

## Sources
- Gilbert, Christina / Y Combinator (2026). "Why You're Getting Zero Replies To
  Your Cold Emails." <https://www.youtube.com/watch?v=wr6PMD06hP0> —
  [[2026-09-12-yc-zero-replies-cold-emails|local copy]]
