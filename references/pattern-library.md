# Strategic Experimentation: Pattern Library

**Version:** 0.2
**Status:** Reference. Expected to evolve as the skill is used.
**Purpose:** Reference material for the `strategic-experimentation-coach` skill. The skill draws from this document to (a) recognise good vs. weak inputs from the user, (b) propose options when the user is stuck, and (c) match experiments to the assumptions being tested.

## Changelog

- **v0.2** — Rebalanced Part 4 worked examples to draw from varied domains. Made Part 3 caveat its engagement/retention focus more explicitly. Light edits for plain-prose style.
- **v0.1** — Initial draft synthesised from Cagan, Torres, Bland, Gilad, and Longden/Speero frameworks.

---

## How the skill uses this document

Two layers:

- **General framework layer** (Parts 1–2): the hierarchy, assumption types, experiment ladder, hypothesis formulation. Applies to any product question.
- **Domain layer** (Parts 3–5): patterns tuned to engagement, retention, and content products. Most calls in that domain will land here. Other domains will need their own pattern sets added over time.

When the skill suggests options to the user (e.g. "what strategic hypotheses might answer this?"), it pulls candidates from the relevant patterns, proposes them, and lets the user accept, edit, or add. The skill never blindly accepts what the user provides if it conflicts with these patterns — see `pushback-rules.md` for what to reject and how.

## Provenance

This synthesises several established frameworks. The skill treats them as one integrated approach, naming the lineage only when it adds clarity:

- **Marty Cagan / SVPG (INSPIRED):** the four big product risks — value, usability, feasibility, viability.
- **Teresa Torres (Continuous Discovery Habits):** opportunity solution trees, assumption mapping, "test assumptions, not ideas."
- **David Bland & Alex Osterwalder (Testing Business Ideas):** the experiment library, importance × evidence prioritisation.
- **Itamar Gilad (Evidence Guided / GIST):** the confidence meter, ICE, progressive validation.
- **Jonny Longden / Speero (Apollo Principle, XOS):** the theoretical-question → strategic-hypothesis → functional-hypothesis hierarchy, horse-race iterative learning, systems thinking, the principle that experiments inform decisions but aren't decisions.

---

# Part 1: Framework foundations

## 1.1 The hierarchy

The skill walks users down a five-level hierarchy. Each level constrains the next:

```
Theoretical question   ← What outcome are we trying to influence?
        ↓
Strategic hypothesis   ← Which direction will we bet on to influence it?
        ↓
Functional hypothesis  ← Which lever will we pull in that direction?
   (a.k.a. tactic)
        ↓
Solution               ← What specific thing will we build/do?
        ↓
Experiment             ← How will we test the assumptions?
```

### Definitions and examples

| Level | Definition | Example (retail marketing) |
|---|---|---|
| Theoretical question | A broad outcome-focused question. Open enough to admit multiple directions; narrow enough to be tractable. | *"How can we resonate with a younger audience?"* |
| Strategic hypothesis | A bet on **where** the answer lives — a direction of effort. | *"By changing our product portfolio."* |
| Functional hypothesis (tactic) | A bet on **how** to pull a lever in that direction. Not a feature. | *"By merchandising different products in marketing."* |
| Solution | A specific thing to build/test. | *"Redesign category pages around a younger product mix."* |
| Experiment | A test of the assumptions behind the solution. | *"Web category page A/B test on 10% of sessions for 4 weeks; success = +15% engagement among under-35 cohort."* |

## 1.2 The theory ↔ observation cycle

The hierarchy is presented linearly but operates as a loop. Theory generates strategic and functional hypotheses; experiments produce observations; observations refine the theory. The skill should treat the running map as a living document — when an experiment invalidates an assumption, the relevant branch of the tree changes.

```
   Growth theories  ⇄  Observed behaviour
            ⇅              ⇅
        Experiments & feedback loops
```

## 1.3 Core principle: test assumptions, not ideas

Don't test "the Discover page idea" as a monolithic thing. Decompose it into the assumptions underneath, prioritise by which are riskiest and least supported, and run small targeted tests against those. A single idea often rests on five to ten assumptions; one cheap test can kill the whole idea by invalidating a single load-bearing one.

This is the most commonly skipped step in product teams and the one the skill is built to enforce.

## 1.4 The six assumption types

Every tactic rests on a set of assumptions. The skill helps users surface them, label them, and prioritise testing. The six types:

| Type | Question it asks | Example | Common failure mode |
|---|---|---|---|
| **Problem** | Is the thing we think is broken actually broken? | The cohort genuinely fails to find content they'd engage with. | Assumed without checking existing data. |
| **Root cause** | Is our explanation of why it's broken correct? | The failure is caused by discovery friction, not by lack of interest or time. | Most commonly skipped. Load-bearing — if wrong, nothing built on it works. |
| **Desirability** | Do users want what we're proposing? | The cohort will engage with better-surfaced content if shown. | Often confused with usability. |
| **Mechanism** | Will the specific change produce the response we expect? | A new discovery surface is materially better than what exists today. | Skipped because "obvious." |
| **Magnitude** | Will the effect be big enough to matter at scale? | The cohort-level effect is large enough to be worth shipping. | The "won the A/B test, lost in production" failure. |
| **Value chain** | Does the proximate metric we move actually move the business metric we care about? | Increased on-site discovery → increased depth → increased retention. | Almost never tested. |

Order them in this sequence when designing experiments: cheapest and most upstream first. Killing a tactic via a problem-assumption check costs hours; killing it via a magnitude test costs weeks.

## 1.5 Cross-reference: the six types vs. Cagan's four big risks

The skill uses the six-type framing because it's more granular at the tactic level, but users trained on Cagan will ask. The mapping:

| Cagan risk | Maps to assumption types |
|---|---|
| **Value risk** (will customers buy/use it?) | Problem, Desirability, Magnitude |
| **Usability risk** (can they figure it out?) | Mechanism (when "mechanism" includes UX) |
| **Feasibility risk** (can we build it?) | Not directly covered — out of scope at tactic level; addressed at solution level |
| **Business viability risk** (does it work for the business?) | Value chain, Magnitude |

**The Cagan pattern**: teams systematically over-index on feasibility (the comfortable, engineer-friendly one) and under-index on value and viability. The skill should flag if a user's assumption list is all feasibility-flavoured.

Beyond Cagan's four, the skill should also surface other risk categories from systems-level thinking (Longden):

- **Technical risk** — will this break something else?
- **Operational risk** — how does this impact workflows or other teams?
- **Customer risk** — could this degrade the overall experience?
- **Brand risk** — does it conflict with positioning?

## 1.6 The horse-race experiment ladder

Ideas earn the right to progress through increasingly rigorous (and expensive) validation. Cost and confidence both rise along the path:

```
Ideas → Analysis → POC → Test Flight → Iterative Development → Full Feature
 £                                                                    ££££
 low confidence                                              high confidence
```

The shape of the funnel matters: most ideas should die early. If everything makes it to "Full Feature," the team isn't horse-racing — they're rubber-stamping.

**Key principle (Longden):** the fidelity and rigor of an experiment must match the cost and irreversibility of the potential failure. A button colour test? Low fidelity is fine. Killing a free tier? Test-flight-level rigor before going live.

## 1.7 The validation methods matrix

Methods organised by validation category × fidelity (adapted from Speero):

| Category | Low fidelity (cheap learning) | Mid fidelity | High fidelity (real-world) |
|---|---|---|---|
| **Problem & discovery** | User interviews, surveys, analytics audits | Ethnographic studies, journey mapping | — |
| **Concept & value prop** | Concept tests (discussion), ad creative tests, value-prop surveys | Landing page tests ("painted door"), clickable mockups | — |
| **Solution & experience** | Wireframe reviews, paper prototyping | Interactive prototype tests, remote usability tests | In-person usability tests, beta program |
| **Feasibility & operational** | Internal estimates, technical spikes | Internal simulations, technical prototypes | Operational pilots, data integration tests |
| **Market & business model** | Acquisition channel tests (small), pricing concept surveys | Beta launches, phased rollouts (small segment), simulated pricing | Pilot programs, larger phased rollouts, live pricing tests |
| **Optimisation & refinement** | Usability audits, analytics review | Session recording analysis, user feedback tools | A/B tests, multivariate, personalisation, funnel analysis |

A/B tests sit at the bottom right — they're the most expensive and slowest-to-learn-from option. Use them when cheaper methods can't answer the question, not as the default.

## 1.8 Matching experiments to assumption types

| Assumption type | Best experiment types (cheap → expensive) |
|---|---|
| **Problem** | Analytics segment comparison, funnel analysis, support-ticket review, then user interviews |
| **Root cause** | Diary studies, moderated user sessions, behaviour clustering, then matched-pair analytics |
| **Desirability** | User interviews, surveys, fake-door tests, concept tests, then concierge MVP |
| **Mechanism** | Clickable prototypes, Wizard of Oz, then A/B test |
| **Magnitude** | Hard to test cheaply. Cohort projections from analogous past launches, then small-segment rollout, then full A/B |
| **Value chain** | Causal-leaning cohort analysis on existing users, matched-pair comparisons, propensity score matching |

## 1.9 Confidence ratings

Borrowed from Gilad's Confidence Meter. For each assumption, label the evidence level:

- **High** — multiple independent sources of evidence (data + research + analogous case)
- **Medium** — directional evidence from one or two sources, or strong analogous evidence
- **Low** — opinion, intuition, or single anecdote
- **None** — never examined

The targets for testing are the **low-confidence and high-importance** assumptions. High-confidence ones can usually be left alone; low-importance ones aren't worth the test even if uncertain.

## 1.10 Experiments inform decisions; they aren't decisions

A critical Longden point: an experiment produces evidence, not a verdict. The team takes the evidence, combines it with other inputs (qualitative research, strategic context, systems-level considerations, brand and operational risks), and makes a human decision.

This matters because it means experiment output should be framed as input to a decision, not "the test won, ship it." The skill's experiment-design phase should always include a "decision criteria" section: *if X happens, we will Y; if Z happens, we will W*.

## 1.11 LOFAs — Leap of Faith Assumptions

Within an assumption list, some assumptions are "load-bearing" — if they're wrong, the entire tactic collapses. Borrowed from lean-startup vocabulary as **Leap of Faith Assumptions** (LOFAs). The skill should explicitly identify which assumptions are LOFAs and ensure those get the most rigorous testing earliest.

A useful test: *"If I learned tomorrow that this assumption was wrong, would I kill this tactic, or would I just adjust the solution?"* If the answer is "kill the tactic," it's a LOFA.

## 1.12 Growth experiments vs optimisation

Two distinct modes (Longden):

- **Optimisation** — incremental improvement within a known framework. A/B tests on button colour, copy variants, layout tweaks. Cheap, fast, low strategic stakes.
- **Growth experiments** — validating significant, high-uncertainty strategic hypotheses. Should something new exist? Will this new proposition land? Should we change our business model?

This skill operates in the **growth experiment** mode. Optimisation work doesn't need the full theoretical-question → strategic-hypothesis decomposition — it can go straight to test design. The skill asks early which mode the user is in, and if it's pure optimisation, suggests skipping straight to Phase 5 (experiment design).

---

# Part 2: Question and hypothesis patterns

## 2.1 Theoretical question patterns

### Good shapes
- *"How can we [outcome] for [segment]?"* — most flexible.
- *"Why do [users] [behaviour]?"* — opens root-cause exploration.
- *"What's stopping [segment] from [behaviour]?"* — generative.
- *"How do we move [metric] from [X] to [Y] by [timeframe]?"* — when the metric is genuinely the goal, with quantification.

### Anti-patterns

| Anti-pattern | Example | Reframe |
|---|---|---|
| Names a solution | *"Should we build a Discover page?"* | *"How can we make content easier to discover?"* |
| Yes/no question | *"Should we cut the free tier?"* | *"What would happen if we changed our free-tier strategy?"* |
| Pure metric target with no outcome framing | *"How do we get to 1M DAU?"* | *"How can we grow our active user base among [segment]?"* |
| Too broad | *"How do we grow?"* | *"How do we grow [specific cohort] over [timeframe]?"* |
| Multiple questions conflated | *"How do we acquire younger users and retain them better?"* | Pick one. They have different answers. |
| About outputs not outcomes | *"How do we ship more features?"* | *"How do we increase engagement?"* (then ask whether feature velocity is the right lever) |

## 2.2 Strategic hypothesis patterns

Strategic hypotheses are bets on the **direction** of the answer. They should be distinct, not just rewordings of each other, and there should usually be 2–4. Common high-level shapes:

For **engagement / retention** questions:
- Improve existing value (deepen what we have)
- Build new value (add new propositions)
- Change who we target
- Change how we reach them
- Change when we reach them
- Reduce friction in what already exists

For **acquisition** questions:
- New channels
- Better messaging in existing channels
- Better targeting in existing channels
- Lowering the barrier to first try
- Increasing perceived value before sign-up

For **monetisation** questions:
- Pricing structure changes
- Packaging changes
- New propositions for new segments
- Improving conversion at existing decision points
- Reducing leakage (cancellation, downgrade)

The skill should propose 3–5 strategic hypotheses appropriate to the question type, then let the user refine.

## 2.3 Functional hypothesis (tactic) patterns

Functional hypotheses are levers within a strategic direction. They should be at a "verb-phrase" altitude — describing the lever, not the implementation. The test of altitude: *can you generate 3+ specific solutions from this tactic?* If not, it's probably a solution disguised as a tactic.

Examples of good tactics under "improve existing value" for an engagement question:
- *Reduce friction of finding the content users specifically want*
- *Make existing core touchpoints (home, index, article) more engaging*
- *Increase awareness of value propositions users don't currently use*
- *Make it easier to discover content users might enjoy but haven't found*

Examples of things that look like tactics but are actually solutions:
- *Build a Discover page* (solution — many possible tactics could lead here)
- *Add a TL;DR box* (solution)
- *Personalise the homepage* (closer to a tactic, but still implementation-flavoured)

## 2.4 The if-then-because hypothesis statement

The skill restates each priority tactic as a falsifiable hypothesis:

> **If** [we do X], **then** [Y will happen], **because** [A, B, and C are true].

Variants:
- *"We believe that [X] will achieve [Y] for [segment], because [A, B, C]."* (Bland format)
- *"In order to achieve [outcome], we will [tactic]. We will know this is working when [signal]. Our key assumptions are [A, B, C]."*

### Requirements for a good hypothesis statement

- **Specific X**: not "improve onboarding" but "personalise the first-session homepage based on declared interests"
- **Measurable Y**: a metric with a direction, ideally with a threshold or order of magnitude
- **Falsifiable**: there must be an observation that would prove it wrong
- **Multiple, distinct because-clauses**: one clause = one assumption = one possible thing to test
- **No conflated assumptions**: "users want this and will use it weekly" is two assumptions

### Examples

**Weak:**
> *If we add a Discover page, then engagement will go up, because users will find more content.*

Problems: vague X, vague Y, single conflated because-clause, no segment specified, no measurable signal.

**Strong:**
> *If we add a personalised Discover surface to the homepage for cool subscribers, then weekly engagement depth (articles read per session) will increase by 10–15% within that cohort over 4 weeks, because (a) cool subscribers currently fail to find content matching their interests, (b) that failure is caused by lack of personalisation rather than catalogue gaps, (c) when shown personalised content, cool subscribers engage with it at rates similar to warm subscribers, and (d) the lift in articles-per-session correlates with our retention metric.*

Each clause is now a separately testable assumption.

---

# Part 3: Common assumption sets by tactic type

These are starter sets for common tactic categories. They lean toward engagement/retention product work — other domains will need their own pattern sets added over time. The skill proposes these as candidates; the user edits.

## 3.1 Discovery / findability tactics

Examples: Discover page, homepage personalisation, search improvements, content recommendations, cross-product discovery.

**Typical assumption set:**
1. *(Problem)* The cohort genuinely fails to find content they'd engage with — observable in their current behaviour, not just inferred.
2. *(Root cause — usually the LOFA)* The failure is due to discovery friction, not lack of time, lack of interest, or content-catalogue gaps.
3. *(Desirability)* Better-surfaced content would actually be consumed, not just seen.
4. *(Mechanism)* The proposed discovery surface is meaningfully better than what exists today.
5. *(Magnitude)* The lift is large enough to matter at cohort level, not just per-session.
6. *(Value chain)* More content discovered → more engagement depth → improved retention metric.

**Common skipped assumption:** #2. Teams treat the discovery-friction explanation as obvious. It often isn't.

## 3.2 On-content engagement tactics

Examples: adaptive article layouts, new storytelling formats, TL;DR boxes, audio versions, in-article features.

**Typical assumption set:**
1. *(Problem)* The cohort is arriving at content but disengaging before getting value.
2. *(Root cause)* The on-page experience is what's causing disengagement (not headline mismatch, not device context, not topic disinterest).
3. *(Root cause)* This cohort has on-page needs distinct from engaged users.
4. *(Mechanism)* The proposed intervention addresses the actual friction point.
5. *(Magnitude)* The proximate metric we'd move (scroll depth, completion rate) is sensitive enough to detect a real change.
6. *(Value chain)* The proximate metric correlates with the business metric.

**Common skipped assumption:** #2. Teams design article-level interventions when the disengagement happens at headline-click or context-mismatch level.

## 3.3 Off-platform touchpoint tactics

Examples: newsletter sign-ups, push notifications, podcast promotion, social presence.

**Typical assumption set:**
1. *(Value chain — usually the LOFA)* The touchpoint causally drives return visits, not just correlates with them. Selection bias is huge here.
2. *(Problem)* The cohort isn't sufficiently exposed to or signed up for the touchpoint.
3. *(Desirability)* The cohort will sign up when given better placement/defaults.
4. *(Desirability)* Once signed up, the cohort will actually engage with the touchpoint (open rate × CTR).
5. *(Mechanism)* The proposed sign-up surface materially outperforms current.
6. *(Magnitude)* The new sign-ups translate into measurable return-visit lift at cohort level.

**Common skipped assumption:** #1. Almost universal in product teams. The skill should aggressively flag this.

## 3.4 New value proposition tactics

Examples: new product features, new content formats, new propositions for new segments.

**Typical assumption set:**
1. *(Problem)* There's an unmet need this addresses.
2. *(Desirability)* The cohort would value the proposition.
3. *(Desirability)* They'd value it enough to change behaviour (visit more, pay more, stay longer).
4. *(Mechanism)* The proposed implementation delivers on the proposition.
5. *(Magnitude)* The addressable cohort is large enough to matter.
6. *(Value chain)* Adoption translates to the target business metric.
7. *(Risk)* It doesn't cannibalise an existing higher-value proposition.

**Common skipped assumption:** #3 (intensity of desire) and #7 (cannibalisation).

## 3.5 Onboarding / activation tactics

Examples: improved onboarding flow, tooltips, declaring preferences, first-session experience.

**Typical assumption set:**
1. *(Problem)* New users are dropping off before reaching value.
2. *(Root cause)* The drop-off is because of friction or unclear value, not because they signed up for the wrong reason.
3. *(Desirability)* Users will engage with the onboarding rather than skip it.
4. *(Mechanism)* The onboarding intervention removes the friction or makes value clearer.
5. *(Value chain)* Onboarding completion → activation → retention.

**Common skipped assumption:** #2. The "wrong reason for signing up" failure mode is invisible to A/B testing.

---

# Part 4: Worked examples

These show the framework in action across different domains. The point of having more than one is to show that the same hierarchy applies whether the question is about retail marketing, content engagement, or something else.

## 4.1 Worked example: Resonating with a younger audience (retail / marketing)

This example is drawn from Speero's framework material. The team is a retailer wanting to expand their audience to younger customers.

**Theoretical question:** *How can we resonate with a younger audience?*

**Strategic hypothesis A:** *By changing our product portfolio*
- *By merchandising different products in marketing* — tactic
- *By cutting out certain product ranges from the portfolio* — tactic

**Strategic hypothesis B:** *By targeting a younger audience in media*
- *By restricting advertising to channels where audiences can be targeted* — tactic
- *By modifying messaging/tone in creative* — tactic

The two strategic hypotheses sit at the same altitude but address different levers (what we sell vs how we communicate). Tactics under each describe how to pull a lever in that direction, not specific implementations.

From there, each tactic generates candidate experiments:
- *Web category page experiment* — under "merchandising different products"
- *eCRM experiment* — also under merchandising
- *SEO evaluation / biz case* — under "cutting out product ranges"
- *Google Shopping Feed Test* — also under product portfolio
- *PPC targeting experiment* — under "restricting advertising"
- *Paid social targeting experiment* — also under media targeting
- *Web landing page experiment* — under "modifying messaging/tone"
- *Qualitative user testing* — also under creative messaging

The discipline: each experiment tests assumptions specific to its parent tactic, not "does the whole young-audience strategy work?" Tests stay small and targeted.

## 4.2 Worked example: Engagement frequency in a content product

Here's how the same framework decomposes for a subscription content product wanting to raise return-visit frequency among low-engagement subscribers.

**Theoretical question:** *How can we increase engagement frequency among casual and low-engagement subscribers?*

**Strategic hypothesis A:** *By improving mechanisms that bring them back to the app/website*
- *By improving the quality of push notifications*
- *By improving the quality of other off-platform touchpoints (newsletters, podcasts)*
- *By increasing the reach of off-platform touchpoints (more sign-up surfaces, better defaults)*
- *By improving session continuity (logged-in state, recognised devices)*

**Strategic hypothesis B:** *By giving them new reasons to come / removing reasons not to*
- *By making our platform the only place to get certain content*
- *By distributing content on platforms where users already are*
- *By introducing new incentives (or removing penalties/friction)*

Two things worth noting in this map:

1. **Strategies A and B are alternative bets, not sequential steps.** The team will pick one direction to invest in, not pursue both.
2. **The B-strategy's first and second tactics actively contradict each other** — "only available here" vs "distribute widely." That's correct at this level. They're alternatives to choose between via experimentation, not a contradiction to resolve in advance.

For comparison: an engagement-*depth* tree for the same product would look different. Strategic hypotheses about value propositions, content quality, and discovery would dominate, rather than the touchpoint/reach hypotheses that fit frequency.

## 4.3 Frequency vs depth in content products

Engagement in content/subscription products usually decomposes into two largely orthogonal axes:

- **Frequency** — how often does the user return?
- **Depth** — how much do they engage in each visit?

Strategic hypotheses cluster differently for each. Frequency-side hypotheses are usually about touchpoints, habits, and reasons to return (off-platform mechanisms, push, newsletters, exclusive content). Depth-side hypotheses are usually about value, discovery, and on-content experience.

When a user presents a theoretical question that mixes the two, the skill should ask them to split it — they need different hypotheses and different metrics.

## 4.4 The engagement temperature model

For products with varied user engagement levels (subscription content, SaaS, marketplaces), cohort segmentation by engagement state helps target the right strategic hypotheses:

- **Hot** — highly engaged, frequent, deep. Don't optimise primarily for this group; you'll get false positives because they engage with almost anything.
- **Warm** — engaged, regular. Worth growing but already converted to the proposition.
- **Cool** — sporadic, low depth. Often the biggest opportunity for engagement-depth work.
- **Cold** — barely engaging. Often a retention/reactivation problem, not an engagement problem.

The temperature of the cohort affects which strategic hypotheses are sensible. A "build new value" hypothesis is wasted on cold users who never see the new value. A "remove friction" hypothesis is wasted on hot users who don't experience the friction.

The skill should ask which cohort the work is targeting and check that the proposed hypotheses are appropriate for that cohort.

---

# Part 5: Anti-patterns and traps

The skill should watch for these and flag them to the user.

## 5.1 The feasibility over-index (Cagan)

Teams systematically pick assumptions and experiments engineers are comfortable with — technical spikes, prototypes, build-and-A/B-test. They under-invest in value and viability questions, which are scarier and harder. If a user's assumption list has zero desirability or value-chain assumptions, push back hard.

## 5.2 Metric thinking vs systems thinking (Longden)

Picking the highest-projected-impact initiative without considering systems effects. Classic case: aggressive price-cuts boost short-term revenue (Initiative #1, +$50k) while eroding brand perception (Initiative #1, –$80k over 18 months, invisible in the quarter).

When a user proposes a tactic, ask: *what are the second-order effects? What might this break elsewhere? What's the downstream impact on other metrics or brand?* If the answer is "I haven't thought about it," that's a value-chain assumption gap.

## 5.3 Sense-checking vs experimenting (Longden)

"We A/B tested the feature when we shipped it" is not experimentation — it's sense-checking. By the time the feature is built, the assumptions baked in are already mostly determined. Real experimentation happens before the build, testing the assumptions that justify the build.

The skill enforces this by requiring assumption-level testing before solution design.

## 5.4 "Vibes-based" prioritisation

Tactics get prioritised by gut-feel and presentation polish rather than evidence. The pushback rules require explicit confidence ratings and evidence citations; this exists to disrupt vibes-based prioritisation. When a user rates an assumption "high confidence" with no evidence cited, the skill should challenge: *what's the evidence?*

## 5.5 "Ship and pray"

Building the full feature, releasing, watching metrics, hoping. The horse-race ladder exists to prevent this. The skill should always propose the cheapest test first, even when the user wants to skip to "let's just build it." Cost-of-failure framing helps: *if this is wrong and we ship it, what does it cost to roll back, and what's the brand/customer impact?*

## 5.6 A/B testing as innovation

A/B tests are an optimisation tool, not an innovation tool. They tell you which of two variants is better within a known framework. They don't tell you whether you should be in that framework at all. For genuinely novel propositions, A/B testing is the wrong method — you need qualitative validation first, then concept tests, then prototype tests, then A/B as the final check.

## 5.7 Mistaking correlation for causation in value-chain assumptions

"Newsletter subscribers return 4x more often than non-subscribers." Almost certainly inflated by selection bias — people who sign up were already going to return more. The skill should always require causal-leaning evidence (matched-pair, propensity-matched, or quasi-experimental) for value-chain assumptions, not raw correlations.

---

## Notes for future iteration

- Add patterns for paid/monetisation tactics when relevant.
- Add patterns for B2B/enterprise products.
- Add patterns for e-commerce, marketplace, and platform products.
- Consider adding a section on cohort segmentation methods.
- Build a library of real completed-experiment cases as the skill is used.
- Speero's UX heuristics (Value, Relevance, Clarity, Friction, Motivation) could become a structured prompt for generating tactics under "improve existing on-platform value" strategic hypotheses.
