---
source: agent
compiled_from:
  - agent-notes/raw/business/entrepreneurship/2026-11-04-how-to-talk-to-users.md
  - agent-notes/raw/business/entrepreneurship/2026-11-04-collect-stories-not-generalizations.md
  - agent-notes/raw/business/entrepreneurship/2026-11-04-how-to-talk-to-users-alstromer.md
  - agent-notes/raw/business/entrepreneurship/2026-11-05-best-customer-interview-questions.md
compiled_at: 2026-11-05
model: claude-fable-5-1
confidence: medium
---

# Customer Interviews

**Customer interviews** — YC's phrase is "talking to users" — are the founder-run conversations that turn a hunch about a problem into hard facts about how specific people actually experience it. Eric Migicovsky (Pebble founder, YC partner) gave the canonical Startup School treatment in 2019, and is explicit that most of it is a synthesis of Rob Fitzpatrick's *The Mom Test* (2013). His framing: YC's teaching reduces to two activities, write code and talk to users, and the second is the one founders systematically outsource or do badly. The lecture supplies three things: the errors to avoid, five questions that work at any stage, and a different *purpose* for interviewing at each of the three pre-product-market-fit stages (idea, prototype, launched). Allen Pike's 2023 essay on **story orientation** tightens the second error: a problem-side question that asks people to generalize about themselves fails almost as badly as a hypothetical, and the repair is to ask for one recent episode. Gustaf Alströmer (YC group partner, earlier a product lead at Airbnb) re-recorded the Startup School talk under the same title in 2022. It has less of the theory and more of the two ends Migicovsky leaves thin: how to get the conversation in the first place, and what to do with the notes once there are five or ten sets of them. Teresa Torres, whose book Pike draws on, adds the planning step in a 2022 Product Talk post: keep the list of things you want to learn to yourself, and ask for the one story that answers them.

## Founders do this themselves

Migicovsky's opening claim is organizational, not tactical: the best companies are the ones where the founders keep a direct line to users for the company's whole life. Hiring salespeople or heads of product does not discharge the obligation — "if you are the CEO it is in your job description." The engineer-founder is not exempt either; he invokes the *Office Space* go-between ("I have people skills!") as the role you must never need to hire. The implicit argument is about information loss: an interview's value lies in specific, unprocessed detail (who, when, which class, which file), and every hand-off between the person who heard it and the person deciding what to build strips some of that detail away. This is the same reason [[early-stage-startup-execution]] insists the founder makes the cold calls, and why [[design-partners]] treats early users as research subjects the founder studies personally.

Alströmer makes the same claim through Airbnb, where he worked. He sets the coding-montage scene from *The Social Network* against a photograph of Brian Chesky with Amol Surve, whom he calls the very first guest, taken over a weekend the two spent together in San Francisco. Only the second picture, he says, shows "a two-way conversation with a real customer." In 2010 Chesky gave up his apartment to live in what Alströmer counts as 50 different Airbnbs over a couple of months. The press read it as a stunt; Alströmer reads it as a way to talk to a different host every day. Chesky and Joe Gebbia also put their personal cell numbers on the website for hosts, and by his account still take those calls. His counter-example is a search of your own inbox for "do-not-reply@", which lists the companies that have chosen not to hear from their customers.

His reason for the discipline is incentive, where Migicovsky's is information loss: users and customers "are the only stakeholders actually paying you anything," so "if anyone will tell you the truth it will be them." That holds best for people who already pay. A few minutes later he says that people who know you "can be less honest in their answers to not offend you," which is the Mom Test problem below.

## The three Mom Test errors

Fitzpatrick's title names the failure: pitching your idea to someone who loves you and wants to support you, then mistaking their encouragement for data. Migicovsky distils the book to three mistakes founders "pretty much all" make:

1. **Talking about your idea instead of their life.** An interview is for extracting information, not selling. The goal is specifics about the problem area as the user lives it, including the path that led them to the problem and their motivations for being there at all. Alströmer calls this "the most important thing" in the interview: hold the idea back until the end of the call, "or maybe not at all," because hearing it biases the answers.
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

## Alströmer's set: six questions, three follow-ups, five to avoid

Alströmer builds his version around a mock startup. The hypothesis, which he calls an idea space, is that companies want to cut their carbon emissions and for some reason do not. His six questions, with X standing for the task or goal:

| Alströmer's question | Nearest Migicovsky question | What differs |
|---|---|---|
| 1. Tell me how you do X today. | None | Process before pain. The workflow, tools and people are on the table before anyone has named a problem. |
| 2. What is the hardest thing about doing X? | Question 1 | Same. |
| 3. Why is it hard? | Question 3 | Same. |
| 4. How often do you have to do X? | The prototype-stage frequency number | Asked in the first conversation instead of held for later. |
| 5. Why is it important for your company to do X? | None | The one he says to "dive deep" on. It tests whether the task matters, which is a separate question from whether it hurts. |
| 6. What do you do to solve this problem for yourself today? | Question 4 | Same, with an addition: if they can share a screen and show you, "that's even better." |

His list has no counterpart to "tell me about the last time" or to "what don't you love about the solutions you've tried."

Question 5 earns its place in his filmed demo. "Amy," a former Airbnb colleague, says her company does care about its emissions and pays a consultant for a PDF report once a year. Asked what they do with the report: "I don't think we really take much action on it." Asked why the company tracks emissions at all, she mentions regulation on the way (the captions drop the first half of her answer). On this article's reading, that answer moves the hypothesis. He started with companies that want to reduce emissions and do not. The demo shows a company that has to report and does not act, which is a different problem to build for.

He pairs the list with three follow-ups, on the grounds that nobody says everything in one answer: "What do you mean by that?", "Can you tell me more about that?" and "Why is that important to you?" In the demo it is "tell me more about that" that gets from "the information is really dense" to detail a builder can use: the consultant sends a Word document to fill in, the data going into it "seems inaccurate," and the company feels it would need "another expert" to act on the result.

The questions he says derail an interview:

| Avoid | His reason |
|---|---|
| "Will you use our product?" | They will probably say yes, and the yes means nothing. |
| "Which features would make product X better?" | Their job is to tell you about the problem. Deciding the features is yours. |
| Yes/no questions | You want explanation and "concrete and real examples." |
| "What would a better product X look like to you?" | Most interviewees are not designers, engineers or product managers. They have a different job, and you are there to learn the hard part of it. |
| Two questions at once | It confuses them and muddies the answer. It happens when you are eager. |

The first is Mom Test error 2. The second and fourth are error 1 from the other side: asking the user to do the founder's job. The third and fifth are rules of question craft that Migicovsky's lecture does not state. The fifth is what survey designers call a double-barreled question: the interviewee answers the easier half and the notes do not show which.

His own demo opens with a yes/no question, "Do you care about your carbon emissions?" It worked because Amy volunteered the consultant and the report along with her yes, and everything useful after that came from open follow-ups. An interviewee who answers only "yes" leaves nothing to follow up on.

## Feature requests are symptoms

Alströmer's "one big danger" is letting the interview drift from problems to features, which he says comes naturally because the founder's brain is already solving. His rule: "users generally have good problems but also generally bad solutions." Two examples:

- **Gmail.** Early users asked Paul Buchheit for a view showing the inbox and the open message on the same screen. The reason was speed: Gmail was slow, and they did not want to wait for each email to load.
- **Airbnb.** Early guests asked for hosts' phone numbers. "Why do you need that?" turned up that they did not yet trust the platform and wanted to get to know the host before booking.

In both, building the request would have treated the symptom (a split pane, a phone field) and left the cause (latency, trust) in place. His second argument is about incentives. Users have no reason to say no to a feature, so three proposed features collect three yeses, while the founder carries the cost of building them and has to prioritize.

Migicovsky's question 5 and the faster horse say not to *ask* for features. Alströmer covers the case where the request arrives unasked: treat it as a report that something is wrong and ask why, which is his third follow-up put to work.

## Stories, not generalizations

Allen Pike (2023) argues that moving from solution questions to problem-space questions is necessary but not sufficient. "How often do you struggle with X?", "What do you take into account when choosing Y?" and "Why don't you use approach Z?" pitch nothing and imagine no future, and by his account they still tend to produce untrue answers. Each one asks the interviewee to summarize their own behavior. His fix, taken from Teresa Torres's *Continuous Discovery Habits* (2021), is **story orientation**: ask for one recent, specific episode instead. Torres's own account of how to choose that episode is the next section.

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
- **Alströmer's list splits the same way.** "How often do you have to do X?" and "why is it important for your company?" ask for summaries, and "tell me how you do X today" becomes one unless it is pinned to an instance ("walk me through the last time"). His own demo is the jeans example again: "do you care about your carbon emissions?" got "we do actually care," and "what do you do with the report?" got "I don't think we really take much action on it."
- **Watching outranks the story.** Alströmer's "ideal state" is a screen share in which the interviewee opens the PDF report and shows how they get it and what they do with it. A story still passes through memory and an observed walkthrough does not, so the order of evidence runs generalization, story, observation. His reason is practical: "changing the behavior will be hard," so the founder needs to see exactly what behavior the product has to displace.
- **Fitzpatrick already had the category.** *The Mom Test* files generic claims ("I usually," "I always," "I never") under fluff, next to future-tense promises and hypothetical maybes. Migicovsky's lecture compresses that into one line about discarding fluff at the launched stage. Pike's contribution is to make it the organizing rule for every stage and to say why it happens.
- **The gap between the two answers is data.** Pike's caveat is that the self-deception still matters for marketing: a problem people do not know they have is harder to sell a fix for. The generalization is the self-image the copy has to speak to; the story is the behavior the product has to serve. A jeans retailer would advertise fit and compete on brand and price.
- **One story is one data point.** A recent episode can be unrepresentative, and Pike concedes stories carry their own memory errors. Story orientation does not remove the need to generalize; it moves the generalizing from the interviewee, who does it badly about themselves, to the interviewer, who does it across many episodes and many people. Pike's closing test is the practical check: reread the notes and count how many lines are stories.

## Research questions are not interview questions

Torres's "Ask Teresa" post (Product Talk, 2022) is her own short version of the method Pike borrowed, and it supplies the step his essay assumes: how to get from what you want to know to what you say. She says teams conflate two lists.

- **Research questions** are what you are trying to learn. Her Netflix example: what do you like to watch, where, with whom, on what device.
- **Interview questions** are what you ask in the room to learn it.

Put a research question to a customer and they will answer it. Her objection is that a direct question out of context draws a fast response that "feels true, but often it's not," and that nobody is trying to deceive. Pike's two mechanisms in the previous section are a fuller account of the same failure. Torres leaves the science to a separate post ("Why You Are Asking the Wrong Customer Interview Questions"), which is not ingested here.

Her method is to look across the research questions and ask, "What's a specific story I can collect that will get me answers to those questions?" The interview is then spent collecting that story, and the interviewer listens for the answers inside it. For Netflix the prompt is "Tell me about the last time you watched Netflix." One story covers what, where, with whom and on which device, and none of the four is asked.

**The outcome sets the scope.** The prompt widens or narrows with what the team is responsible for:

| The team's outcome | Opening prompt |
|---|---|
| Find new market opportunities | "Tell me about the last time you did something fun." |
| Netflix viewing in general (her default) | "Tell me about the last time you watched Netflix." |
| Mobile | "Tell me about the last time you watched Netflix on the go." |

Her two cautions: the Netflix prompt is too narrow for a team looking for brand-new products, and too wide for the mobile team, who would hear "a whole bunch of stories about watching Netflix on a TV."

**The target opportunity sets the depth.** Once the team picks an opportunity to work on, the prompt stays the same and the attention moves. For "I can't tell if this show is any good," she would spend longer on the part of the story where the person chose what to watch and less on the watching. She still asks for the whole story, so that the team keeps learning about the rest of the opportunity space.

**The golden rule.** "Let the participant talk about what they care about most." Some participants have no relevant story, want to tell a different part of it, answer in one sentence, or want to list feature requests and gripes about the product. Her instruction is to capture what they are willing to share and not force the rest. Her reason is cadence: a team that interviews every week will talk to another customer soon, so "a disappointing interview is easily forgotten."

How this fits the rest of the article (this article's reading, not Torres's):

- **Alströmer's learning goals are research questions, and his demo asks one.** He writes down "does the company care about its emissions" before the call, then opens it with "Do you care about your carbon emissions?" That is the conflation Torres describes, and it explains why the opening only worked because Amy volunteered more than a yes. Torres's version would open on an episode, something like "tell me about the last time emissions came up at your company," and listen for the three goals (do they care, why, who cares most) in what follows.
- **Migicovsky's five reorder around question 2.** "Tell me about the last time" opens the interview. The other four become things to listen for in the episode, or follow-ups on it ("why was that hard?", "what did you do about it?"), and stop being questions asked cold.
- **The scope dial is how a product-team method reaches a founder.** Torres writes for teams that have a product and a pool of customers to recruit from every week. A founder at the idea stage has neither, which puts them in her widest case, the team looking for new markets. The prompt should be set wider than the idea: about the job the person does, not the product that might help with it. Alströmer's "idea space" is the same width. The narrower prompts belong to the prototype and launched stages, when there is a product whose use can be asked about.
- **The golden rule sits against "discard bad data."** Migicovsky says to steer fluff back to specific episodes. Torres says to try, then let go. Feature requests are where the two meet: Alströmer's "why do you need that?" is the steering attempt, and Torres's rule covers the interviewee who will not be steered.
- **Her reason for letting go depends on volume.** At one interview a week for a year, a wasted one is 2% of the evidence. At the five or ten interviews Alströmer buckets into a hypothesis, it is 10–20%. Her argument still points the same way for the founder: book the next interview, do not push harder in this one.

## Idea stage: find the first people with the problem

Before any product exists the aim is simply to find people who have the problem and will describe it.

- **Start with yourself.** Many of the best products are built for the founder; run the interview on your own last encounter with the problem first.
- **Then friends and coworkers, by warm intro.** A research program begins with one or two people, not thousands; what matters is that the interview is unbiased and detailed, not that it is numerous.
- **Just show up.** A YC company selling to firefighters got nowhere with cold email, so they walked into fire stations unannounced, asked for the chief, and got dozens of 10–15 minute meetings. Migicovsky's reframe for the discomfort: if you genuinely think you are solving their problem, taking fifteen minutes of their day is a favor to them.
- **Industry events, guerrilla-style.** Pebble went to CES with no booth and no budget and set up meetings in the conference coffee shop, because the people they needed were concentrated there.

Tips for the stage: take detailed notes (you will not know until later which fact mattered), bring a co-founder or ask to record, keep it casual rather than calendar-blocked, expect the first five or ten interviews to change your process dramatically, and respect the other person's time — a first interview of 10–15 minutes is usually enough.

Alströmer adds the steps that come before the first question:

- **Write down what you want to learn.** For the carbon startup: does the company care about its emissions; why, or why not; and who inside it cares most, and why. The third locates the buyer. It is the idea-stage form of the authority question in the prototype stage below. In Torres's terms all three are research questions: kept on the page, and listened for instead of asked.
- **Who to ask, easiest first.** People you know are the most likely to reply and the most likely to soften their answers. Coworkers and former coworkers often know the domain. Past both circles, the channels YC founders named to him most often were LinkedIn, Reddit, Slack and Discord communities, and in-person events. For the mock startup he looks on LinkedIn for founders, CEOs and CFOs, and for titles containing carbon, climate or sustainability.
- **The message.** To a CFO he once worked with: who I am, what we share, that I am starting something new, described briefly "but not too much in detail," and one ask, a 20-minute phone or video call. The cold version has the same parts in a different tone. The small, specific ask is the call to action [[cold-outbound]] recommends for sales email. The message names the area and holds back the solution, which keeps it consistent with error 1. In the demo he says only that he has "a couple questions" about an area he is interested in.
- **Talk live, and build rapport.** Video, phone or in person: "you can learn a lot more from a five minute video interview" than from 500 or 5,000 survey responses. The interviewee is about to answer questions "maybe no one" has asked them before, so they need to trust the person asking.

Migicovsky's idea-stage interview is 10–15 minutes, casual, sometimes a walk-in. Alströmer's is a scheduled 20-minute call. On this article's reading the gap follows the interviewee (classmates and fire chiefs versus CFOs reached over LinkedIn) and is not a disagreement about method.

## From notes to a hypothesis

Migicovsky goes from interviews straight to the prototype. Alströmer describes the step between. After five or ten interviews:

1. Have notes from every one.
2. Sort what was said into buckets, one per problem, on sticky notes or in software.
3. See which bucket matters most.
4. Write the conclusions down.
5. Turn them into a hypothesis about the solution.

He warns against over-intellectualizing this. The aim is to start designing the [[minimum-viable-product]] quickly, on accurate information, and then to test it "with the same users."

He adds a check on whether the problem is **valuable**, meaning people would pay to have it solved:

1. **Is money already changing hands?** If the consultants who produce carbon reports are getting paid, "that's a good sign."
2. **Is there a solution people are happy with, however basic?** Excel and Google Sheets are competitors to "many hundreds of startups," and formidable ones. Nobody pays hundreds of dollars a month for something almost as easy to do in a spreadsheet, so the replacement has to be dramatically better.
3. **How easy is this audience to sell to?** His example is that plumbers and contractors are "notoriously difficult" next to startups, because they rarely change their tools. A valuable problem can sit behind a slow buyer.

How these fit the rest of the article:

- Checks 1 and 2 are Migicovsky's question 4 read across a market, and they pull against each other. Existing spend shows the problem is worth money. Contentment with what the money buys, or with a free spreadsheet, raises the bar for a replacement. The demo passes both: the consultant is paid, and the client cannot act on the report.
- All three look at present behavior. None asks "would you pay?", so the money question gets an answer without a hypothetical.
- They are market-level tests. The cost, frequency and budget numbers in the next section are customer-level. One set decides whether the problem is worth pursuing, the other whom to sell to first.
- Check 3 is a claim about audiences, and it cuts both ways. [[schlep-blindness]] records Graham's argument that founders unconsciously avoid tedious, hard-to-sell markets, which is why those markets stay open. Alströmer is talking about speed of adoption and Graham about competition, so both can be true of the same market. Alströmer does not say to drop such a market, only to weigh the difficulty. The cost shows up as a longer sales cycle and, by Migicovsky's frequency argument below, fewer chances to learn.

## Prototype stage: identify the best first customer

Once there is something to show, the purpose of interviews shifts to choosing *whom to build for first*, because Migicovsky argues the wrong first customer can constrain you or trap you without ever paying. He asks for **numerical answers to three facts**:

1. **How much does the problem cost them today?** A hard number — revenue they would gain, or expense currently wasted, by solving it.
2. **How frequently do they encounter it?** Hourly, daily, quarterly, yearly. Frequent problems win twice: the customer feels the pain more often and is more receptive, and you get more cycles to learn whether the product is working. Pebble's daily-wear habit was his own leading indicator — a watch left in the drawer meant something was wrong.
3. **How large is their budget, and do they have the authority to spend it?** The assembly-line operator feels the problem hourly but cannot buy the fix; their boss in headquarters can.

Picture the three as overlapping circles with the best first customer at the center. His worked example is a smart blender pitched to the French Laundry (high value per sale, low frequency, a sous-chef with no budget), a Google café (high volume but the food is free, so no revenue motive and no budget), and McDonald's (low value per transaction, enormous frequency across thousands of stores, and a warm intro to someone controlling a multi-billion-dollar budget). Put the answers in a three-column spreadsheet and stack rank.

This maps almost exactly onto the Amble/Li screen in [[design-partners]]: frequency is their *urgency*, budget-plus-authority is their *capacity*, and cost-today is what makes a partner representative of a paying market rather than a curiosity. The operator-versus-boss warning is the mirror image of their "CEOs are a capacity trap" — in both cases the lesson is to interview the person who can both feel the problem and fund the solution, and to notice when those are two different people. It is also the concrete version of the problem-discovery lens in [[product-management-framework]]: go deep with interviews, but score what comes back.

## Prototype sessions and the customer group

Migicovsky uses the prototype stage to pick a customer. Alströmer uses it to watch people use the thing. A click-through design prototype is enough. He names InVision, which shut down at the end of 2024; a Figma prototype does the same job now. At Airbnb the team would go downstairs, find people waiting for an interview or a coffee, and hand them a phone showing screens that had not been built. His two rules:

- **Give a goal, not instructions.** "Try to make a booking," or "search with dates." Never say how to get through a screen, because in the real product nobody is standing next to the user.
- **Have them think aloud.** They narrate each step and read out the words in front of them, which shows which words they understand and what they think each screen is for.

This is the think-aloud usability test, and it answers a narrower question than the interviews do. People in an office lobby can show whether a person gets through the flow. They cannot show whether anyone wants it. For that he sends the founder back to the people already interviewed.

He also says to keep those interviewees involved, usually through a Slack workspace or a WhatsApp group, which he says many YC companies run with their customers:

- Word the invitation so members feel they have exclusive early access.
- Keep showing them the product as it progresses.
- Ship a new screen in response to something they said, so they learn that their feedback is acted on quickly. He says this is what builds trust.
- Let them meet each other. Some will value talking to people who do the same job, which they rarely get to do.

The group is a light version of the cohort in [[design-partners]], without the selection screen or the conversion step.

## Launched stage: a leading indicator for product-market fit

Migicovsky's complaint about the standard PMF definitions — Graham's "something people want," Andreessen's "the product is being pulled out of you" — is that they are vague and retroactive: you have to already have PMF to know you have it, so they cannot guide the next week's work. He points to Rahul Vohra's account of building Superhuman's "product-market fit engine" (First Round Review, 2018; see [[product-market-fit]]) as the fix: ask a sample of users (30–40 is enough) every week, *how would you feel if you could no longer use the product?* — very disappointed, somewhat disappointed, not disappointed — and track the share answering *very disappointed*. Those are the users for whom the product has become habit. The threshold Vohra adopted is 40%: companies at or above it tended to grow on their own, and the weekly measurement tells you whether last week's features moved the number. (The talk credits "some analysis" for the threshold; it originates with Sean Ellis's growth surveys.)

Three tactical tips for this stage:

- **Ask for a phone number high in the signup flow.** When the aggregate data says 20% of users hit some problem, the fastest way to understand it is to call one of them. Alströmer's Airbnb story runs the same line in the other direction: the founders' numbers on the site, so hosts could call them.
- **Don't design by committee.** Instead of "would you use this feature?", put an upgrade flow in front of them that asks for a credit card *before* the feature is built. Payment intent is the only hypothetical worth collecting.
- **Discard bad data.** Compliments ("I love the new design") are not specific or actionable. Fluff — hypotheticals and generic statements about what the product could become — should be steered back to specific past episodes.

## Assessment

Migicovsky's lecture is a compression of *The Mom Test* with YC war stories layered on, and it inherits the book's strengths and one of its gaps. Alströmer's is closer to a field manual.

- **Strength: it is entirely problem-side.** Every question asks about the past and about pain; none pitches. That discipline is what makes the output usable as evidence rather than encouragement, and it is why the five questions survive contact with any industry.
- **Gap: commitment.** Fitzpatrick's book spends a chapter on asking for *commitment and advancement* (time, reputation, money) as the antidote to compliments. The talk reaches for this only at the launched stage with the credit-card test; at the idea and prototype stages it leaves "would they pay?" implicit in the cost and budget numbers. [[startup-ideation-framework]] fills the hole bluntly with its ten-paying-customers test, and [[design-partners]] deliberately excludes willingness-to-pay from selection and reintroduces it at conversion — a sequencing Migicovsky's three-stage model would agree with but does not state. Alströmer never asks for money either. He offers two substitutes: look at what the interviewee already pays someone else, and keep them in a group where staying is a small, repeated commitment of time.
- **The two YC talks cover different halves.** Migicovsky is stronger on what to ask and on what each stage is for. Alströmer is stronger on what happens before the call (learning goals, who, the message) and after it (buckets, the value check, prototype sessions, the group). Taken alone, his question list is the weaker of the two: it leaves out "tell me about the last time" and includes "how often," whose cost the story-orientation section explains.
- **Torres's post is the shortest statement of the method, and the narrowest.** One story prompt, scoped to what the team is responsible for, with the question lists kept as a checklist for listening. It assumes customers already exist and can be reached weekly. Recruiting and synthesis are left to other posts its intro links to, and commitment is not mentioned. For those, the two YC talks here are the fuller sources.
- **Caveat on question 4.** "Nobody is already trying to solve it" is a strong filter against problems people do not feel, and usually correct. It can also screen out categories users have resigned themselves to; the honest reading of the Dropbox example is that the people hacking rsync were the signal of latent demand, not the market. Treat an empty answer as a flag to probe harder on frequency and cost, not as an automatic kill.
- **The frequency point does double duty.** Migicovsky's second reason to prefer frequent problems — more learning cycles — is underappreciated relative to the first. It is an argument about the founder's *information* rate, not the customer's pain, and it connects to the search-not-execution framing in [[minimum-viable-product]] and [[commit-and-go-deep]]: a daily-use product tells you every day whether you are wrong.
- **Pebble is the cautionary footnote to its own example.** It passed the frequency test (worn daily), shipped roughly two million watches, and still ran out of cash in 2016 and sold its assets to Fitbit. Interviewing well tells you the problem is real and who to build for first; it does not protect the business model.

## Sources
- Migicovsky, Eric (2019). "How to Talk to Users." Y Combinator Startup School. <https://www.youtube.com/watch?v=MT4Ig2uqjTc> — [[2026-11-04-how-to-talk-to-users|local copy]]
- Pike, Allen (2023). "Collect Stories, Not Generalizations." <https://allenpike.com/2023/stories-generalizations-product-interviewing/> — [[2026-11-04-collect-stories-not-generalizations|local copy]]
- Alströmer, Gustaf (2022). "How To Talk To Users." Y Combinator Startup School. <https://www.youtube.com/watch?v=z1iF1c8w5Lg> — [[2026-11-04-how-to-talk-to-users-alstromer|local copy]]
- Torres, Teresa (2022). "Ask Teresa: What Are the Best Customer Interview Questions?" Product Talk. <https://www.producttalk.org/best-customer-interview-questions/> — [[2026-11-05-best-customer-interview-questions|local copy]]
