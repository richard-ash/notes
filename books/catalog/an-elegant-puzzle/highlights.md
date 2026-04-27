# An Elegant Puzzle — Highlights

## 1 Introduction

> Organizational design gets the right people in the right places, empowers them to make decisions, and then holds them accountable for their results.

## 2 Organizations

> When I have a problem that I want to solve quickly and cheaply, I start thinking about process design. A problem I want to solve permanently and we have time to go slow? That's a good time to evolve your culture. However, if process is too weak a force, and culture too slow, then organizational design lives between those two.

### 2.1 Sizing teams

> I've sponsored quite a few teams of one or two people, and each time I've regretted it. To repeat: I have regretted it every single time. An important property of teams is that they abstract the complexities of the individuals that compose them. Teams with fewer than four individuals are a sufficiently leaky abstraction that they function indistinguishably from individuals.

> Keep innovation and maintenance together. A frequent practice is to spin up a new team to innovate while existing teams are bogged down in maintenance. I've historically done this myself, but I've moved toward innovating within existing teams. This requires very deliberate decision-making and some bravery, but in exchange you'll get higher morale and a culture of learning, and will avoid creating a two-tiered class system of innovators and maintainers.

### 2.2.1 Four states of a team

> A team is falling behind if each week their backlog is longer than it was the week before. Typically, people are working extremely hard but not making much progress, morale is low, and your users are vocally dissatisfied. A team is treading water if they're able to get their critical work done, but are not able to start paying down technical debt or begin major new projects. Morale is a bit higher, but people are still working hard, and your users may seem happier because they've learned that asking for help won't go anywhere. A team is repaying debt when they're able to start paying down technical debt, and are beginning to benefit from the debt repayment snowball: each piece of debt you repay leads to more time to repay more debt. A team is innovating when their technical debt is sustainably low, morale is high, and the majority of work is satisfying new user needs. Teams want to climb from falling behind to innovating, while entropy drags them backward. Each state requires a different tact.

### 2.2.2 System fixes and tactical support

> I can't stress enough that these fixes are slow. This is because systems accumulate months or years of static, and you have to drain that all away. Conversely, the same properties that make these fixes slow to fix make them extremely durable once in effect!

### 2.2.3 Consolidate your efforts

> Adding new individuals to a team disrupts that team's gelling process, so I've found it much easier to have rapid growth periods for any given team, followed by consolidation/gelling periods during which the team gels. The organization will never stop growing, but each team will.

### 2.3.1 Team first

> Fundamentally, I believe that sustained productivity comes from high-performing teams, and that disassembling a high-performing team leads to a significant loss of productivity, even if the members are fully retained. In this worldview, high-performing teams are sacred, and I'm quite hesitant to disassemble them.

### 2.3.4 Shift scope; rotate

> Shifting scope works better than moving people because it avoids re-gelling costs, and it preserves system behavior. Preserving behavior keeps your existing mental model intact, and if it doesn't work out, you can always revert a workload change with less disruption than would be caused by a staffing change. The other approach that I've seen work well is to rotate individuals for a fixed period into an area that needs help. The fixed duration allows them to retain their identity and membership in their current team, giving their full focus to helping out, rather than splitting their focus between performing the work and finding membership in the new team. This is also a safe way to measure how much slack the team really has!

### 2.4.3 Ways to manage entropy

> My favorite observation from *The Phoenix Project* by Gene Kim, Kevin Behr, and George Spafford is that you only get value from projects when they finish: to make progress, above all else, you must ensure that some of your projects finish. That might imply that there is an easy solution, but finishing projects is pretty hard when most of your time is consumed by other demands.

> Finally, the one thing that I've found at companies with very few interruptions and have observed almost nowhere else: really great, consistently available documentation. It's probably even harder to bootstrap documentation into a non-documenting company than it is to bootstrap unit tests into a non-testing company, but the best solution to frequent interruptions I've seen is a culture of documentation, documentation reading, and a documentation search that actually works.

> Finally, a related antipattern is the gatekeeper pattern. Having humans who perform gatekeeping activities creates very odd social dynamics, and is rarely a great use of a human's time. When at all possible, build systems with sufficient isolation that you can allow most actions to go forward. And when they do occasionally fail, make sure that they fail with a limited blast radius.

## 3 Tools

### 3.2.3 Solution validation

> Once you've narrowed down the problem you want to solve, it's easy to jump directly into execution, but that can make it easy to fall in love with a difficult approach. Instead, I've found that it's well worth it to take the risk out of your approach with an explicit solution validation phase. The elements that I've found effective for solution validation are: Write a customer letter. Write the launch announcement that you would send after finishing the solution. Are you able to write something exciting, useful, and real? It's much more useful to test it against your actual users than to rely on your intuition. Identify prior art. How do peers across the industry approach this problem? The fact that others have solved a problem in a certain way doesn't mean that it's a great way, but it does at least mean it's possible. A mild caveat: it's better to rely on people you have some connection to instead of on conference talks and such, since there is a surprisingly large amount of misinformation out there. Find reference users. Can you find users who are willing to be the first users for the solution? If you can't, you should be skeptical whether what you're building is worthwhile. Prefer experimentation over analysis. It's far more reliable to get good at cheap validation than it is to get great at consistently picking the right solution. Even if you're brilliant, you are almost always missing essential information when you begin designing. Analysis can often uncover missing information, but it depends on knowing where to look, whereas experimentation allows you to find problems that you didn't anticipate. Find the path more quickly traveled. The most expensive way to validate a solution is to build it in its entirety. The upside of that approach is that you've lost no time if you picked a good solution. The downside is that you've sacrificed a huge amount of time if it's not. Try to find the cheapest way to validate. Justify switching costs. What will the costs of switching be for users who move to your solution? Even if folks want to use it, high switching costs may mean that they simply won't be able to. Test with your potential users if they'd be willing to pay the full cost of migrating to your solution instead of their existing planned work.

### 3.3.1 Strategies and visions

> Strategies are grounded documents which explain the trade-offs and actions that will be taken to address a specific challenge. Visions are aspirational documents that enable individuals who don't work closely together to make decisions that fit together cleanly.

### 3.6.2 Running good migrations

> The good news is that while migrations are hard, there is a pretty standard playbook that works remarkably well: de-risk, enable, then finish.
>
> • **De-risk** The first phase of a migration is de-risking it, and to do so as quickly and cheaply as possible. Write a design document and shop it with the teams that you believe will have the hardest time migrating. Iterate. Shop it with teams who have atypical patterns and edge cases. Iterate. Test it against the next six to twelve months of roadmap. Iterate. After you've evolved the design, the next step is to embed into the most challenging one or two teams, and work side by side with those teams to build, evolve, and migrate to the new system. Don't start with the easiest migrations, which can lead to a false sense of security. Effective de-risking is essential, because each team who endorses a migration is making a bet on you that you're going to get this damn thing done, and not leave them with a migration to an abandoned system that they have to revert to. If you leave one migration partially finished, people will be exceedingly suspicious of participating in the next.
>
> • **Enable** Once you've validated the solution that solves the intended problem, it's time to start sharpening your tools. Many folks start migrations by generating tracking tickets for teams to implement, but it's better to slow down and build tooling to programmatically migrate the easy 90 percent. This radically reduces the migration's cost to the broader organization, which increases the organization's success rate and creates more future opportunities to migrate. Once you've handled as much of the migration programmatically as possible, figure out the self-service tooling and documentation that you can provide to allow teams to make the necessary changes without getting stuck. The best migration tools are incremental and reversible: folks should be able to immediately return to previous behavior if something goes wrong, and they should have the necessary expressiveness to de-risk their particular migration path. Documentation and self-service tooling are products, and they thrive under the same regime: sit down with some teams and watch them follow your instructions, then improve them. Find another team. Repeat. Spending an extra two days intentionally making your documentation clean and your tools intuitive can save years in large migrations. Do it!
>
> • **Finish** The last phase of a migration is deprecating the legacy system that you've replaced. This requires getting to 100 percent adoption, and that can be quite challenging. Start by stopping the bleeding, which is ensuring that all newly written code uses the new approach. That can be installing a ratchet in your linters, or updating your documentation and self-service tooling. This is always the first step, because it turns time into your friend. Instead of falling behind by default, you're now making progress by default. Okay, now you should start generating tracking tickets, and set in place a mechanism which pushes migration status to teams that need to migrate and to the general management structure. It's important to give wider management context around migrations because the managers are the people who need to prioritize the migrations: if a team isn't working on a migration, it's typically because their leadership has not prioritized it. At this point, you're pretty close to complete, but you have the long tail of weird or unstaffed work. Your tool now is: finish it yourself. It's not necessarily fun, but getting to 100 percent is going to require the team leading the migration to dig into the nooks and crannies themselves. My final tip for finishing migrations centers around recognition. It's important to celebrate migrations while they're ongoing, but the majority of the celebration and recognition should be reserved for their successful completion. In particular, starting but not finishing migrations often incurs significant technical debt, so your incentives and recognition structure should be careful to avoid perverse incentives.

## 4 Approaches

### 4.3.1 An ethical profession

> I believe that management, at its core, is an ethical profession. To see ourselves, we don't look at the mirror, but rather at how we treat a member of the team who is not succeeding. Not at the mirror, but at our compensation philosophy. Not at the mirror, but at how we pitch the roles to candidates. Whom we promote. How we assign raises. Provide growth opportunities. PTO requests. Working hours. We have such a huge impact on the people we work with—and especially on the people who work "for" us—and taking responsibility for that impact is fundamental to good management.

### 4.3.2 Strong relationships > any problem

> I believe that almost every internal problem can be traced back to a missing or poor relationship, and that with great relationships it is possible to come together and solve almost anything. Technical disagreements become learning opportunities for everyone. Setbacks are now a shared experience that offers the opportunity to gel together as a team. Even with great relationships, there are still real challenges! You have a limited budget for giving raises and can't satisfy everyone. If your customers don't love your product, camaraderie can't pay salaries. Some technical problems are genuinely novel, without an obvious solution, and sometimes the obvious solution is cost-prohibitive. That said, I try to start debugging problems from the relationship angle, and I find this technique pretty effective.

### 4.3.3 People over process

> A few years back, one of the leaders I worked with told me, "With the right people, any process works, and with the wrong people, no process works." I've found this to be pretty accurate. Process is a tool to make it easy to collaborate, and the process that the team enjoys is usually the right process. If your process is failing somehow, it's worth really digging into how it's failing before you start looking for another process to replace it.

### 4.7 Finding managerial scope

> As managers looking to grow ourselves, we should really be pursuing scope: not enumerating people but taking responsibility for the success of increasingly important and complex facets of the organization and company. This is where advancing your career can veer away from a zero-sum competition to have the largest team and evolve into a virtuous cycle of empowering the organization and taking on more responsibility. There is a lot less competition for hard work.

## 5 Culture

### 5.6.3 A long time coming, a long time going

> One of the observations from systems thinking is that, though humans are prone to interpreting events as causal, often problems are better described in terms of a series of stockpiles that grow and shrink based on incoming and outgoing flows. The Dust Bowl wasn't caused by one farmer or one year of overfarming, but by years of systemic abuse. Stocks and flows are especially valuable in understanding the failure of projects and teams. Projects fall behind one sprint at a time. Technical debt strangles projects over months. Projects fail slowly—and fixing them takes time, too. Working at a frenetic pace for a couple of weeks or a month may feel like a major outpouring of effort and energy, but it's near impossible to quickly counteract a deficit created over months of poor implementation or management choices.

## 6 Careers

> Luck plays such an extraordinary role in each individual's career progression that sometimes the entire concept of career planning seems dubious. However, as managers, we have an outsize influence in reducing the role of luck in the careers of others. That potential to influence calls us to hold ourselves accountable for creating fair and effective processes for interviewing, promoting, and growing the folks we work with.

### 6.2 Running a humane interview process

> I'm confident that the state of interviewing is improving: many processes now involve a prepared presentation on a technical topic instead of an impromptu presentation (this more closely replicates a real work task), and many have replaced the whiteboard algorithm problem with a period of collaborative pair programming on a laptop with your editor of choice.

> Reflecting on the interviews I've run over the past few years and those I got to experience recently, I believe that, while interviewing well is far from easy, it is fairly simple. Be kind to the candidate. Ensure that all interviewers agree on the role's requirements. Understand the signal your interview is checking for (and how to search that signal out). Come to your interview prepared to interview. Deliberately express interest in candidates. Create feedback loops for interviewers and the loop's designer. Instrument and optimize as you would any conversion funnel.

### 6.2.3 Finding signal

> Just identifying the signals you want is only half of the battle, though; you also need to make sure that the interviewer and the interview format actually expose that signal. It really depends on the signal you're looking for, but a few of the interview formats that I've found very effective are: Prepared presentations on a topic. Instead of asking the candidate to explain some architecture on the spur of the moment, give them a warning before the interview that you'll ask them to talk about a given topic for 30 minutes, which is a closer approximation of what they'd be doing on the job. Debugging or extending an existing codebase on a laptop (ideally on their laptop). This is much more akin to the day-to-day work of development than writing an algorithm on the board. A great problem can involve algorithmic components without coming across as a pointless algorithmic question. (One company I spoke with had me implement a full-stack auto-suggest feature for a search inbox, which required implementing a prefix tree, but the interviewer avoided framing it as yet another algo question.) Giving demos of an existing product or feature (ideally the one they'd be working on.) This task helps them learn more about your product and get a sense of whether they have interest around what you're doing, and it helps you get a sense of how they deliver feedback and criticism. Roleplays (operating off a script that describes the situation.) This option can be pretty effective if you can get the interviewers to buy into it, allowing you to get the candidate to create more realistic behavior (architecting a system together, giving feedback on poor performance, running a client meeting, and so on). More than saying that you should specifically try these four approaches (but you should!), the key point is to keep trying new and different approaches that improve your chance of finding signal from different candidates.

### 6.2.5 Deliberately express interest

> Make sure your candidates know that you're excited about them. I first encountered this idea reading Rands's "Wanted" article, and he does an excellent job of covering it there. The remarkable thing is how few companies and teams do this intentionally: in my last interviewing process, three of the companies I spoke with expressed interest exceptionally well, and those three companies ended up being the ones I engaged with seriously.

> Whenever you extend an offer to a candidate, have every interviewer send a note to them saying that they enjoyed the interview. (Compliment rules apply: more detailed explanations are much more meaningful.) At that point, as an interviewer, it can be easy to want to get back to your "real job," but resist the temptation to quit closing just before you close: it's a very powerful human experience to receive a dozen positive emails when you're pondering if you should accept a job offer.

### 6.3.1 Moving beyond your personal networks

> Many hiring managers freeze up when their referral network starts to dry up, or as they look to bring a wider set of backgrounds onto their teams. However the good news is that there is a simple answer: cold sourcing. Cold sourcing, a technique that's also common in some kinds of sales, is reaching out directly to people you don't know. If you're introverted, this will probably be an extremely unsettling experience at first, with questions like "What if they're annoyed by my email?" and "What if I'm wasting their time?" ringing in your head. These are important questions, and we have an obligation to be thoughtful about how we inject ourselves into others' lives. I was personally paralyzed by this concern initially, but ultimately I think it was unfounded: a concise, thoughtful invitation to discuss a job opportunity is an opportunity, not an infringement, especially for those who are on career networking sites like LinkedIn. Most folks will ignore you (which is great), others will politely demur (also great), a few will actually respond (even greater), and a surprising number will ignore you for six months and then pop up mentioning that they're starting a new job search. I've never had someone respond unkindly. The other great thing about cold sourcing is that it's pretty straightforward.

### 6.3.3 Is this high-leverage work?

> Similarly, a frequent follow-up question is whether sourcing is a high-leverage task for engineering managers. I think it is: candidates are more excited to chat with someone who'd be managing them than they are to chat with a recruiter whom they'll mostly work with during the interview process. Likewise, I think it's a valuable signal showing that managers care about hiring enough to invest their personal energy and attention into it.

> As a closing thought, the single clearest indicator of strong recruiting organizations is a close, respectful partnership between the recruiting and engineering functions. Spending some time cold sourcing is a great way to build empathy for the challenges that recruiters face on a daily basis, and it's also an excellent opportunity to learn from the recruiters you partner with! We've been doing weekly cold sourcing meetings as a partnership between our engineering managers and engineering recruiters, and it's been a great forum for learning, empathy-building, and, of course, hiring.

### 6.4.3 Extending the funnel

> Instead of ending your funnel at closing candidates, add four more phases: Onboard. How long does it take new hires to get up to speed? It's pretty tricky to measure this, but since you're trying to reason about the population rather than individuals, it's okay to be a bit messy. Pick a productivity metric, maybe commits per week, and see how long it takes for new hires to reach P40 productivity. That's a sufficiently good measure for understanding how long it takes folks to ramp up. Impact. How impactful are the people that you're hiring? Again, that's a tricky one to measure, but you're looking to understand trends, not individuals, so don't worry about identifying perfect metrics. A reasonably good proxy here is looking at the performance rating distribution for new hires based on time since hiring. Promote. How long does it take individuals to get promoted after they're hired? This is useful for understanding whether employees have access to opportunity within your organization. Retain. Are the people you hire staying? Fortunately, this one is pretty easy to track by looking at the people who leave. It is, however, quite a lagging indicator, since it typically takes years for folks to leave. Still, I believe that it's an essential metric to track. Not many companies extend their hiring funnel this way, but I think it's quite useful, reframing hiring from a transactional process into your organization's lifeblood. It's also true that many companies are very uncomfortable sharing this kind of information widely. That's fine. These are indeed quite sensitive numbers, but you should make sure someone is paying attention to them.

### 6.5.1 Career ladders

> A good ladder allows individuals to accurately self-access; these ladders are self-contained and short. A bad ladder is ambiguous and requires deep knowledge of precedent to apply correctly. If there is one component of performance management that you're going to invest into doing well, make it the ladders: everything else builds on this foundation.

### 6.5.2 Performance designations

> Somewhat unexpectedly, performance designations are usually not meant to be the primary mechanism for handling poor performance. Instead, feedback for weak performance should be delivered immediately. Waiting for performance designations to deal with performance issues is typically a sign of managerial avoidance. That said, it does serve as an effective backstop for ensuring that these kinds of issues are being addressed.

## 7 Appendix

### 7.1.3 Managing an organization

> The mechanism I've found most helpful in this case is to ensure that every team has a clear set of directional metrics in an easily discoverable dashboard. The metrics should cover both the longer-term goals of the team (user adoption, revenue, return users, etc.) and the operational baselines necessary to know if the team is functioning well (on-call load, incidents, availability, cost, and so on.) For each metric, the dashboard should make three things clear: the current value, the goal value, and the trend between them.

> The other mechanism I've found to be exceptionally useful at this point is team snippets. These come out every two to four weeks and give snapshots of each team's sprints: what they're doing, why they're doing it, and what they're planning to do next. These are valuable for you to retain a sense of what your teams are working on, but they are invaluable for decentralizing coordination and communication between teams in your organization, as you become increasingly ineffective in that role.
