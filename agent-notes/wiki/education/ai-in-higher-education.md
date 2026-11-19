---
source: agent
compiled_from:
  - agent-notes/raw/education/2026-11-19-impacts-of-ai-in-higher-education.md
compiled_at: 2026-11-19
model: claude-fable-5-2
confidence: medium
---

# AI in higher education

How undergraduates use generative AI, what they think it does to their learning, and what they expect it to do to their jobs. The anchor source is the first wave of the **Dartmouth AI Survey** (Sacerdote and Parris-Bacon, 2026), a panel survey fielded June to September 2026. Its picture: AI use is routine, most of it is study help, students agree it damages writing and has broken take-home assessment, and they are almost entirely self-taught. Its most distinctive result is a large gap between the misuse students admit to and the misuse they attribute to classmates.

Everything here is **self-report from one non-peer-reviewed working paper**. The numbers describe what students say, not what they do.

## The survey

Three samples answered similar, not identical, instruments:

| Sample | N | Notes |
|---|---|---|
| Current Dartmouth undergraduates | 1,201 | Classes of 2026 to 2029, $20 gift card, Qualtrics |
| Incoming Dartmouth students | 332 | Class of 2030, asked before arrival about their high school |
| U.S. college students | 1,003 | College Pulse panel at four-year colleges, anonymized |

The Dartmouth sample matches the college on Pell eligibility (21%) but over-represents women (56% against 50%) and international students (26% against 13%). Majors: 9% humanities, 27% social sciences, 44% sciences. The authors are also surveying employers, with the option of an AI voice interviewer built by Expected Parrot, to test whether student beliefs about jobs match what firms report.

## What students use AI for

The paper sorts uses into "potentially helpful" and "potentially harmful" to learning. Self-reported use among Dartmouth undergraduates:

- **Helpful:** explaining difficult concepts 66%, checking AI answers against other sources 62%, generating practice quizzes and study aids 57%, grammar and proofreading 53%, finding sources 37%, outlining 37%, math problems 36%, code 35%.
- **Harmful:** summarizing assigned readings 43%, drafting essays 17%, finding problem-set answers without understanding them 9.5%, copy-pasting AI text with little editing 5.4%.

63% say a back-and-forth with AI produces a better result than either the AI or the student alone (52% in the U.S. sample). In the appendix, 77% to 88% of students by division say they have started a task with AI and then deliberately finished it themselves to protect their learning. That is the behaviour the [[ai-judgment-atrophy]] argument says people will not sustain, so it is a number worth watching in later waves.

The national figures are consistent with other surveys the paper tabulates: Gallup and Lumina find 57% of U.S. undergraduates use AI for coursework at least weekly, and the HEPI survey finds 94% of U.K. undergraduates use it on assessed work.

## The self versus peer gap

Each use was asked twice: do you do this, and do your peers do this?

| Harmful use | Dartmouth self | Dartmouth peers | U.S. self | U.S. peers |
|---|---|---|---|---|
| Drafting essays or papers | 17.0 | 63.4 | 23.0 | 54.5 |
| Copy-pasting with little editing | 5.4 | 37.6 | 8.0 | 49.7 |
| Summarizing assigned readings | 43.2 | 75.5 | 39.3 | 59.7 |
| Problem-set answers without understanding | 9.5 | 41.6 | 10.6 | 49.4 |

The authors offer two explanations and think both operate:

1. **Under-reporting.** Students will not incriminate themselves. Meta-analyses of sensitive behaviours put under-reporting at about 40% in the worst cases (Lensvelt-Mulders et al., 2005).
2. **Over-estimating peers.** A few egregious, memorable incidents inflate beliefs about the typical classmate.

Their evidence that under-reporting is not the whole story: the gap is just as large in the anonymized College Pulse sample; doubling the self-reports still leaves a large gap; and in focus groups students themselves described an even mix of the two.

Two qualifications the paper does not make. First, the doubling test fails for summarizing readings, where twice the self-report exceeds the peer figure in both samples, and it nearly closes the U.S. essay-drafting gap (46 against 54.5). Second, the authors say self and peer rates "match up quite nicely" for helpful uses, citing concepts (66 against 72), quizzes (57 against 66) and grammar (53 against 69). The same table shows gaps above 28 points for code, outlines, math and paying for premium tools. So students attribute more of *every* use to peers, and the peer inflation is not specific to cheating.

**Why the gap matters even if the truth is unknowable.** The belief does the damage. 70% of both samples say take-home work has become unfair because so many students use AI, and 40% say they feel they have to use AI on out-of-class work because peers do. If peer misuse is overestimated, part of that pressure rests on a false belief, and publishing accurate norms would lower it. This is the logic of pluralistic ignorance and of social-norms interventions on campus drinking. The pressure also looks learned in college: only 14% of incoming students report it about high school, against 37% to 41% in every enrolled class.

## Beliefs about learning and assessment

Share who agree or strongly agree, Dartmouth then U.S.:

- AI use for writing can harm the development of writing skills: 92 / 84
- Take-home essays, problem sets and quizzes are increasingly unfair: 70 / 70
- I feel I have to use AI because so many peers do: 40 / 39
- An instructor's explicit permission or ban guides my use: 75 / 71
- AI helps students understand course concepts more deeply: 70 / 70
- AI makes me more confident in my reasoning: 58 / 66

Students hold the harm and the benefit together. The 75% who say explicit rules guide them is the practical finding for instructors: stated rules are followed far more than the cheating numbers would suggest, and the most common complaint in free text is that rules are unclear (22%) or inconsistent across classes (13%).

## Discipline matters more than class year

Appendix Table A4 gives the mean opinion gap across 24 statements: **17.6 points across academic divisions, 8.9 across class years.** Humanities students are the outliers:

| Statement (Dartmouth) | Humanities | Sciences | Social sciences |
|---|---|---|---|
| AI harms writing skills | 95 | 92 | 92 |
| AI helps understand concepts more deeply | 48 | 70 | 67 |
| AI makes me more confident in my reasoning | 40 | 57 | 56 |
| Strong AI skills will matter for my career | 56 | 78 | 79 |
| I am proactively learning AI skills | 28 | 46 | 47 |
| AI is creating jobs in my field | 21 | 35 | 32 |
| I spend less time with peers because AI answers my questions | 18 | 46 | 36 |

The humanities group is small (about 130 respondents). The authors conclude that "one size does not fit all" and that rules must vary by discipline and course type. One student quote makes the humanities case directly: the best policies were in philosophy classes that banned AI, "because the whole point of philosophy is to struggle."

## Jobs

Dartmouth then U.S.:

- AI is reducing job opportunities in my desired field: 56 / 57
- AI is changing the nature of jobs in my field, not necessarily eliminating them: 84 (Dartmouth only; 88 among incoming students)
- AI is creating jobs in my field: 33 / 32
- Strong AI skills will be important for my career: 74 / 55
- I feel competitive on AI skills: 46 / 53
- I am proactively learning AI skills: 48 (Dartmouth only)

The authors write that "the jobpocalypse has not arrived and is not necessarily coming at all." That sentence rests on student opinion, not employment data, and the students are not unanimous: a majority also say AI is shrinking opportunities in their field. The two answers are compatible with the "task loss, not job loss" reading in [[ai-and-the-future-of-work]] and with Garicano's bundle argument in [[messy-jobs]] (the paper cites the Garicano, Li and Wu book). The contrary evidence the paper itself cites is Brynjolfsson, Chandar and Chen's "Canaries in the Coal Mine?" on early-career employment. The pending employer survey is the first real test.

## Trust

Asked which domains they would never trust AI with, about half of both samples named personal and family decisions. On everything else Table 7 shows Dartmouth students far more willing: financial decisions 7% against 46%, medical 23% against 63%, career or major 5% against 43%.

Treat this comparison as weak. Only 710 Dartmouth students answered, and the paper's own Figure 7 plots different categories and materially different values from Table 7 (for example, roughly 30% of Dartmouth students for financial decisions). The text follows the table.

## Who teaches AI

- 86% of Dartmouth students (79% U.S.) developed their AI skills mostly on their own.
- 53% (68% U.S.) say professors gave meaningful guidance on effective and ethical use.
- 38% (50% U.S.) say their college is adequately preparing them to use AI in a career.

In free text, Dartmouth students asked most for prompting skills (24%), technical application such as coding and automation (23%), and a for-credit course or required workshop (15%). Student-reported examples of good integration share a pattern: the rule is specific and comes with a reason. Use AI "as a peer" (it may clarify, it may not do the assignment); cite AI-written code and comment it to show understanding; generate extra practice problems from the professor's examples; correct in-class writing with AI and then write a reflection on what it changed; draft the course AI policy together with the class.

**High school.** Incoming students describe tight rules: 23% were allowed no AI use at all, 13% could use it to find sources, 6% to summarize readings. The authors suggest that such rules could be counterproductive where AI is in fact good at the task, as with finding scholarly sources.

**Income.** Pell-eligible Dartmouth students are less likely to have paid for premium tools (20% against 30%) but use AI for routine academic tasks at similar rates; Dartmouth provides free access to top-tier tools. They are less likely to say AI skills matter for their career (62% against 77%) or to feel competitive (37% against 48%). Among incoming students, those from more advantaged high schools are about 20 points more likely to say AI deepens understanding and 18 points more likely to use it as a tutor rather than a shortcut. That gap largely disappears among enrolled students, which fits either free access closing it or selection. The paper does not separate the two.

## The authors' prescription

Sacerdote and Parris-Bacon argue that misuse "need not portend the end of higher education":

- **Move assessment into the room.** Many Dartmouth faculty have switched to proctored paper exams without devices. Students say they know they must learn the material because they, not the AI, sit the exam.
- **Spend class and office hours on human interaction.** The authors ban phones, laptops and tablets in class.
- **Use AI as a research assistant outside the room.** Cleaning and merging messy data, or finding the code for a complicated graph, leaves more time for conceptual work. AI also answers office-hours questions when faculty are unavailable.
- **Vary the rules by discipline.** Their own approach is tailored to empirical social science.

This is the complement-not-substitute position of [[intelligence-augmentation]], applied to coursework: keep the reps that build judgment under supervised conditions, and hand AI the work that does not build it.

## Synthesis and open questions

- **Assessment is the binding constraint, not access.** Students already have the tools and already believe the benefits. What has failed is the take-home graded assignment as a measurement instrument. The in-room exam restores measurement at the cost of the long-form, revise-at-home writing that 92% of students say AI is eroding. The paper does not address how writing gets taught once it cannot be graded outside the room.
- **The AI tutor is being used as one.** Explaining difficult concepts is the top use in every sample and every comparison survey. That is the Bloom two-sigma mechanism discussed in [[ai-and-the-future-of-work]] arriving through student initiative, with no evidence yet on learning outcomes. The paper cites studies pointing both ways (Kestin et al. 2025 on AI tutoring outperforming active learning; Bastani et al. 2025 and Strömberg, Lei and Wu 2026 on learning penalties).
- **A training gap colleges are not filling.** 86% self-taught against 38% feeling prepared is the widest institutional gap in the data, and the divide between humanities and other students on proactive skill-building (28% against 46%) suggests self-teaching will widen differences by field.
- **Selection.** Dartmouth is one highly selective college with free premium tools. The U.S. panel differs in instrument, anonymity and incentives, so Dartmouth-versus-U.S. gaps mix real differences with method differences.
- **It is a panel.** The value of the design is future waves: whether the self versus peer gap narrows as norms settle, and whether the class of 2030's low felt pressure (14%) rises once they are on campus.

## Sources
- Sacerdote, Bruce, and Mason Parris-Bacon (2026). "Impacts of AI in Higher Education: A Panel Survey of Undergraduates." NBER Working Paper 36021. <https://www.nber.org/papers/w36021> — [[2026-11-19-impacts-of-ai-in-higher-education|local copy]]
