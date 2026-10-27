---
source: agent
compiled_from:
  - agent-notes/raw/technology/2026-10-26-the-end-of-the-internet.md
compiled_at: 2026-10-27
model: claude-fable-5-1
confidence: medium
---

# Smallness at Scale

The thesis that the open Internet, where anyone could stand up a server and have it count as much as any other, is over, and that the only viable response in every layer it created (publishing, social networking, and now software) has been to go smaller: paid niches instead of ad-funded reach, group chats instead of public feeds, apps for one person or one team instead of the App Store. The anchor source is Ben Thompson's Stratechery essay *The End of the Internet* (2026-10-26). His phrase for the economy that results is "smallness at scale": not one global market but infinite local ones, where "local" may mean a geography or a private network. The essay is an elegy and a forecast at once. Future sources on personal or team-scale software, private networks as the successor to public platforms, or the security economics of self-hosting should integrate here.

## Three endings, one mechanism

Thompson tells the same story three times, a decade apart each time.

**Blogs.** The blogosphere proper began around 2000–2003 (Winer, Hall, Barger and Kottke came earlier; Talking Points Memo, Instapundit, Daily Kos, Daring Fireball, Marginal Revolution and the rest arrived in that window, political blogs first because the politically minded saw that a publication anyone could start and everyone could reach was a radical thing). Free distribution made content abundant, so discovery became the valuable layer and Google captured it, which is [[aggregation-theory]] in its original form. AdSense paid early bloggers for a while, then payouts shrank as inventory went infinite and the best slots stayed on Google's own results page. Thompson's law for this: "because everything is open, everyone has an opportunity, which means infinite competition, which is terrible for business." The survival model was subscriptions. Quoting his own 2015 *Blogging's Bright Future*, a singular voice has a low elasticity of substitution, and a niche is "best served by making more from customers who really care than from milking pennies from everyone." Scarcity is chosen, by limiting the audience on purpose.

**Social media.** Social was the second discovery layer, and for a period Twitter was a community in the old Internet's sense, where "you could reply-guy your way to broader distribution." Entry was even cheaper than blogging, content grew by orders of magnitude, algorithms became necessary, anyone prominent turned defensive, and "community, sadly, doesn't scale." The endpoint is TikTok, "a social media site with basically zero social component." Social *networking* did not die; it moved into group chats, which are familiar, high trust, and "a place where you feel safe to talk," as against the 90-9-1 rule (one percent speak, nine comment, ninety lurk) that governed public social even at its best. The scaling that mattered was "a proliferation of infinite finite groups." Compare [[snapchat]], where Spiegel reweights network effects toward the right people rather than the most people.

**Servers.** The week of the essay produced, by Thompson's list, a remote-code-execution bug in every version of PHP, compromised intermediate certificate-authority private keys (incompetence, he notes, not AI), new vulnerabilities in Node.js, GitLab, Java and Cisco products, a supply-chain breach at LiteLLM, and a breach at the Railway developer platform. His reading: software's gate was always "did it work?", never "is it secure from every privilege escalation or race condition"; attackers used to be bounded by human time and ingenuity; AI removes that bound by substituting iteration for cleverness, and it is getting clever too. The public Internet therefore becomes "a battle zone at best (i.e. social media), and a wasteland at worst (everything else)." Part of this is economic, because AI consumes content and attention "without giving any of the traffic back that Google did," but the technical part is decisive: hosting your own site or app, "the very promise of the Internet," was already dodgy, and "in the age of AI it's madness." Stratechery itself runs on managed WordPress at Pressable and was patched before disclosure. "The Internet as we knew it is dead."

The mechanism under all three is one sentence long. Zero-cost entry produces abundance; abundance hands value to whoever does discovery; the producers beneath face infinite competition; the ones that survive do so by becoming deliberately scarce and small. This is the supplier's-eye view of [[aggregation-theory]]. The third ending adds a twist the first two lacked: AI is the first aggregator that does not route demand back to suppliers at all, which is the same observation [[agents-as-aggregators]] makes when it predicts that apps become "mere suppliers" to an agent.

## The group-chat era of software

Thompson's green shoot. When anyone can make an app, the answer is not the App Store, because "the surge in slop will make the market worse for everyone," but to make something "for yourself and a small group of trusted friends and colleagues." Stratechery has built internal apps for podcast production, task tracking and calendar management, none of which will ever ship publicly, and Thompson has built personal ones for his house and his sports viewing: "it turns out I had a lot of software-shaped holes in my life that suddenly I can fill without asking permission." The economic argument is that software's zero marginal cost always pulled it toward scale, but its large up-front cost meant the audience had to be big enough to justify the build. AI removes the up-front cost, so software for one person or one team becomes viable, and small audiences are "not just a necessity for security, they're an entirely new and potentially much larger market for software creation at scale, by literally everyone."

Read against the existing articles, the claim holds up in shape and needs qualification in degree:

- [[ai-software-output]] (Goedecke) measured exactly this. New software supply rose 2–20× depending on the registry, modest successes roughly doubled, big hits did not move, and the hit rate fell. That is the distribution Thompson predicts: the public market gets worse while the private yield grows.
- [[software-industry-barbell]] (Vernal) puts the light end of the barbell as "people building for themselves or their own company," mostly not venture-addressable, with "the Substack for software" an open question. Thompson's "much larger market" and Vernal's "not venture-addressable" are both true at once: far more value created, little of it capturable by any single vendor.
- [[institutionalized-vs-improvised-software]] (Evans) names the ceiling. Most people are not tool-builders, "knowing what to build is harder than building it," and anything used across departments still has to be bought and decided on. Thompson's apps are improvised software in Evans's sense: one team, no audit trail, no procurement. The institutionalized end does not move.
- [[minimum-viable-saleable-software]] (Leach) prices the part Thompson skips. Verification and maintenance labor, not tokens, is the real cost of a built-not-bought tool, and it recurs. This exposes a tension inside the essay itself: the security section says do not run your own server, the software section says build your own apps. The reconciliation Thompson implies is that "local might mean a private network": apps for one team live behind a firewall or on a managed platform and never face the public Internet. The maintenance burden remains, and he expects AI agents to carry it ("defended by agents continuously").
- [[solopreneur-economy]] (Tedeschi) is the same move at the level of the firm: the viable boundary shrinks to one person, and AI fills the gaps that used to require hiring.

## Cognitive mercantilism and the association

Thompson's optimism rests on Venkatesh Rao's *Cognitive Mercantilism* (Contraptions, the weekend of 2026-10-24; linked, not yet ingested). Rao argues that mercantilism assumed economics was about scarcity and control, and that capitalism arrived when people freed from subsistence farming discovered wants at a scale that pulled whole markets into existence. AI may do the same for "subsistence cognition": from a world where 80% of brains produce intelligence merely to survive to one where 95% satisfy previously unfulfillable cognitive demands. Rao sorts the stances into three: the cognitive mercantilist fears an oversupply of intelligence and a surplus of useless minds; the AI Malthusian expects intelligence to outrun humanity's capacity to absorb it, leaving redundant minds primed for revolt; the cognitive capitalist sees an almost limitless expansion of demand. Thompson takes the third.

He then reaches for Tocqueville's *Democracy in America*: Americans "form associations for the smallest undertakings," and the association, rather than the individual or the state, is the unit through which they act. Markets, Thompson says, are "just another word for needs and desires and the mechanisms of meeting and fulfilling them," and among associations there is not one market but infinite markets, with needs that only arise at the level of the association and that economies of scale cannot serve. The half century of ever-larger corporations and a single global market is, on this reading, the anomaly; the England and America in which capitalism emerged were small-scale and associative.

Connections worth drawing:

- [[distributive-era]] (Arthur) holds that production is solved and distribution is the binding problem. Rao's answer is that demand expands rather than saturates; the two are compatible only if the new demand is met by many small producers rather than a few large ones, which is Thompson's whole point.
- [[ai-and-relational-scarcity]] (Imas) locates post-AI value in goods where human involvement is intrinsic. Group chats and associations are relational goods in that sense, and the exclusivity premium Imas documents is the deliberately-small model with a price on it.
- [[uncopyable-value]] (Kelly) explains why subscriptions worked: they sell patronage and authenticity, which cannot be copied. Kelly's 2026 complaint that findability serves the aggregators rather than creators is Thompson's complaint in a different vocabulary.

## What the essay leaves open

- The security claim is argued from a one-week incident list, not a trend series. The mechanism (AI attackers substitute iteration for cleverness, so the base rate shifts) is plausible and consistent with the list, but it is Thompson's expectation, not a measurement.
- "Potentially much larger market" says nothing about who captures it. Managed hosts (Pressable in Thompson's own practice) and app-building platforms (Lovable, Bolt, Wabi in Vernal's list) are the obvious candidates, which means the aggregator pattern may simply reappear one level down.
- The analogy from group chats to software is weaker than it looks. Group chats won because a universal, free, safe messaging layer already existed. Software for one team needs the equivalent: a hosting and distribution layer cheap and safe enough that a non-builder can run it. That layer is the thing not yet built.
- Thompson is talking his own book; Stratechery is the subscription model's proof case. Discount the enthusiasm, not the pattern, which was visible across all three layers before he had a stake in any of them.

## Sources

- Thompson, Ben (2026-10-26). "The End of the Internet." *Stratechery*. <https://stratechery.com/2026/the-end-of-the-internet/> — [[2026-10-26-the-end-of-the-internet|local copy]]

Referenced in the source but not ingested: Rao, Venkatesh (2026-10). "Cognitive Mercantilism." *Contraptions*. <https://contraptions.venkateshrao.com/p/cognitive-mercantilism>; Thompson, Ben (2015). "Blogging's Bright Future." *Stratechery*. <https://stratechery.com/2015/bloggings-bright-future/>
