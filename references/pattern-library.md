# Strategic Experimentation: Pattern Library

**Version:** 1.0
**Status:** Reference. Expected to evolve as the skill is used.
**Purpose:** Reference material for the `strategic-experimentation-coach` skill. The skill draws from this document to (a) recognise good vs. weak inputs from the user, (b) propose options when the user is stuck, and (c) match tests to the assumptions being tested.

## Changelog

- **v1.0**: Extended onto the full six-level spine (Theoretical question → Strategic hypothesis → Problem hypothesis → Solution hypothesis → MVT → validated/production solution), with a confidence gate at each step. Rewrote §1.1 to the six levels; absorbed the old functional/tactic layer into the problem hypothesis. Replaced the source-count confidence scale (§1.9) with HIGH/MEDIUM/LOW. Added a shared/upstream-LOFA subsection to §1.11, a new §1.13 (the MVT) and §1.14 (the guardrail clause). Added §2.3 problem-hypothesis patterns; replaced the bare if-then-because in §2.4 with the full-format solution statement plus solution-grouping patterns. Relabelled Part 3 "tactic type" as "solution type". Added the in-article-recirculation flagship (§4.1) and the remove-the-units MVT (§4.2) worked examples. Added the targeted-display-ads Cagan-trap fixture (§5.1) and shared-untested-LOFA trap (§5.8). All examples obfuscated for public use.
- **v0.3**: Replaced retail example in §4.1 with fitness-app activation. Swapped §4.2 from content to SaaS. Removed engagement temperature model (§4.4). Rebalanced §1.1, §1.4, §2.3 examples across domains. Loosened §2.4 magnitude and because-clause rules. Removed em dashes throughout.
- **v0.2**: Rebalanced Part 4 worked examples to draw from varied domains. Made Part 3 caveat its engagement/retention focus more explicitly. Light edits for plain-prose style.
- **v0.1**: Initial draft synthesised from Cagan, Torres, Bland, Gilad, and Longden/Speero frameworks.

---

## How the skill uses this document

Two layers:

- **General framework layer** (Parts 1-2): the spine, assumption types, the test ladder, hypothesis formulation. Applies to any product question.
- **Domain layer** (Parts 3-5): patterns tuned to engagement, retention, and content products. Most calls in that domain will land here. Other domains will need their own pattern sets added over time.

When the skill suggests options to the user (e.g. "what strategic hypotheses might answer this?"), it pulls candidates from the relevant patterns, proposes them, and lets the user accept, edit, or add. The skill never blindly accepts what the user provides if it conflicts with these patterns. See `pushback-rules.md` for what to reject and how.

## Provenance

This synthesises several established frameworks plus an applied product operating model. The skill treats them as one integrated approach, naming the lineage only when it adds clarity:

- **Marty Cagan / SVPG (INSPIRED):** the four big product risks: value, usability, feasibility, viability.
- **Teresa Torres (Continuous Discovery Habits):** opportunity solution trees, assumption mapping, "test assumptions, not ideas."
- **David Bland & Alex Osterwalder (Testing Business Ideas):** the experiment library, importance × evidence prioritisation.
- **Itamar Gilad (Evidence Guided / GIST):** the confidence meter, ICE, progressive validation.
- **Jonny Longden / Speero (Apollo Principle, XOS):** horse-race iterative learning, systems thinking, the principle that tests inform decisions but aren't decisions.
- **Applied product operating model:** the six-level spine (theoretical question → strategic hypothesis → problem hypothesis → solution hypothesis → MVT → validated/production solution), the confidence gate at each step, the MVT "validate or kill" framing, the leading/lagging/guardrail metric tiers, and the explicit causal chain to the north-star.

---

# Part 1: Framework foundations

## 1.1 The spine

The skill walks users down a six-level spine. Each level constrains the next, and the work advances only when there is satisfactory confidence at each step (the confidence gate):

```
Theoretical question        ← What outcome are we trying to influence?   (portfolio altitude)
        ↓ confidence gate
Strategic hypothesis        ← Which direction, cohort, and project?       (portfolio altitude)
        ↓ confidence gate
Problem hypothesis          ← What observable behaviour is broken, for whom?
        ↓ confidence gate
Solution hypothesis         ← What one bet fixes that problem?
        ↓ confidence gate
MVT (minimum viable test)   ← The lowest-effort test that validates or kills it
        ↓
Validated / production solution  ← Productionise as MVP; wider test before rollout beyond the cohort
```

The theoretical question and strategic hypothesis are the **portfolio altitude**: they select the cohort and the project before any problem is investigated. The problem → solution → MVT chain sits inside the project the strategic hypothesis selects. The validated/production stage is downstream of the coach's own work (the coach stops at MVT design), but it belongs on the tree as the end state.

**Phase 0 entry at any altitude.** The user need not start at the top. Phase 0 triage routes entry to wherever the user already is: a vague portfolio goal enters at the theoretical question; a chosen direction enters at strategic hypotheses; a known problem enters at problem hypotheses; a fixed solution enters at the solution-hypothesis format and MVT; pure optimisation skips to test design.

### Definitions and examples

| Level | Definition | Example (meal-kit subscription) |
|---|---|---|
| Theoretical question (portfolio) | A broad outcome-focused question that sets the metric family the work must move. | *"How can we lift weekly order rate among light-engagement subscribers?"* |
| Strategic hypothesis (portfolio) | The direction bet that selects the cohort and the project. | *"Reduce churn among light-engagement subscribers by making weekly selection less effortful."* |
| Problem hypothesis | A statement that a specific, observable behaviour is broken for a named cohort, grounded in data. Names a surface or metric, not the fix. | *"For light-engagement subscribers, weekly shortlist completion is markedly lower than for core subscribers, which caps weekly orders."* |
| Solution hypothesis | One falsifiable bet on how to fix the problem, in the full format (§2.4), with its own beliefs and LOFAs. | *"Auto-prepopulate the shortlist from the last three orders, with one-tap edits."* |
| MVT | The lowest-effort test that validates or kills the solution. | *"For weeks 4-12 subscribers, prepopulate the shortlist for half the cohort and read week-on-week order completion against control; agree up front that no lift kills the decision-fatigue premise."* |
| Validated / production solution | After the MVT validates the solution, productionise it as an MVP; run a wider test before rollout beyond the cohort. | *"Roll the prepopulated shortlist to the full light-engagement cohort, then test on adjacent cohorts before global rollout."* |

The old functional-hypothesis (tactic) layer is gone. It is absorbed into the problem hypothesis: the team states solutions concretely, so the verb-phrase tactic altitude is redundant.

## 1.2 The theory ↔ observation cycle

The spine is presented linearly but operates as a loop. Theory generates strategic, problem, and solution hypotheses; tests produce observations; observations refine the theory. The skill should treat the running map as a living document. When a test invalidates an assumption, the relevant branch of the tree changes.

```
   Growth theories  ⇄  Observed behaviour
            ⇅              ⇅
        Tests & feedback loops
```

## 1.3 Core principle: test assumptions, not ideas

Don't test "the new-surface idea" as a monolithic thing. Decompose it into the assumptions underneath, prioritise by which are riskiest and least supported, and run small targeted tests against those. A single idea often rests on five to ten assumptions; one cheap test can kill the whole idea by invalidating a single load-bearing one.

This is the most commonly skipped step in product teams and the one the skill is built to enforce.

## 1.4 The seven assumption types

Every solution rests on a set of assumptions. The skill helps users surface them, label them, and prioritise testing. The seven types:

| Type | Question it asks | Example | Common failure mode |
|---|---|---|---|
| **Problem** | Is the thing we think is broken actually broken? | A cohort of newly signed-up shoppers abandons carts at the payment step. | Assumed without checking existing data. |
| **Root cause** | Is our explanation of why it's broken correct? | Mid-cycle forgetfulness, not lack of intent, drives missed savings goals in a budgeting app. | Most commonly skipped. Load-bearing: if wrong, nothing built on it works. |
| **Desirability** | Do users want what we're proposing? | Subscribers will engage with a prepopulated shortlist if shown by default. | Often confused with usability. |
| **Mechanism** | Will the specific change produce the response we expect? | A relocated tooltip materially reduces drop-off at step 3 of onboarding. | Skipped because "obvious." |
| **Magnitude** | Will the effect be big enough to matter at scale? | A small-segment test lift will hold at full scale. | The "won the A/B test, lost in production" failure. |
| **Value chain** | Does the proximate metric we move actually move the business metric we care about? | Newsletter opens causally drive return visits, not just correlate with them. | Almost never tested. **Now a first-class gate (see VC-GATE-1 in pushback-rules), not an optional check.** |
| **Strategic / scope** | Is the lever we're pulling the right one, vs an adjacent lever? Which surface, which build-vs-iterate, which sub-cohort first? | The right discovery intervention is a new surface vs a component on an existing surface vs iterating existing personalised slots. | Often skipped entirely. Surfaces as "implementation details" mid-build when it's too late to test cheaply. |

Order them in this sequence when designing tests: cheapest and most upstream first. Killing a solution via a problem-assumption check costs hours; killing it via a magnitude test costs weeks. A *strategic / scope* failure tends to be discovered the most expensively of all, usually only noticed when a built thing doesn't move metrics and the team blames the wrong assumption.

**Value-chain is now gated, not optional.** Every solution must carry at least one *stated, mechanism-linked* belief or LOFA connecting the proximate metric to the north-star, written as a falsifiable claim. An item merely present in a list does not clear the gate. A value-chain claim resting only on a raw correlation (held at MEDIUM by the §1.9 cap and §5.7) cannot be the sole gate-satisfier; the gate is not cleared until the causal link is routed to a test. A solution that describes a user problem but never says why fixing it moves the metric fails the gate. This is the operating model's named #1 weakness: most statements are beliefs about the user's problem that never connect why solving it raises the business metric.

**On scope assumptions:** these cover *which lever / surface / sub-cohort to commit to first*, when several plausible options exist and the team has been treating the choice as an implementation detail. Worth proposing whenever a solution could be expressed as "do X to Y" and there are multiple plausible Xs or Ys. They often kill solutions not by being wrong outright, but by causing the team to test the wrong instance of the right idea.

## 1.5 Cross-reference: the seven types vs. Cagan's four big risks

The skill uses the seven-type framing because it's more granular at the solution level, but users trained on Cagan will ask. The mapping:

| Cagan risk | Maps to assumption types |
|---|---|
| **Value risk** (will customers buy/use it?) | Problem, Desirability, Magnitude |
| **Usability risk** (can they figure it out?) | Mechanism (when "mechanism" includes UX) |
| **Feasibility risk** (can we build it?) | Not directly covered, addressed at solution level |
| **Business viability risk** (does it work for the business?) | Value chain, Magnitude |

**The Cagan pattern**: teams systematically over-index on feasibility (the comfortable, engineer-friendly one) and under-index on value and viability. The skill should flag if a user's assumption list is all feasibility-flavoured. See §5.1 for the canonical fixture.

Beyond Cagan's four, the skill should also surface other risk categories from systems-level thinking (Longden):

- **Technical risk**: will this break something else?
- **Operational risk**: how does this impact workflows or other teams?
- **Customer risk**: could this degrade the overall experience?
- **Brand risk**: does it conflict with positioning?

## 1.6 The horse-race test ladder

Ideas earn the right to progress through increasingly rigorous (and expensive) validation. Cost and confidence both rise along the path:

```
Ideas → Analysis → POC → Test Flight → Iterative Development → Full Feature
 £                                                                    ££££
 low confidence                                              high confidence
```

The shape of the funnel matters: most ideas should die early. If everything makes it to "Full Feature," the team isn't horse-racing, they're rubber-stamping.

**Key principle (Longden):** the fidelity and rigour of a test must match the cost and irreversibility of the potential failure. A button colour test? Low fidelity is fine. Killing a free tier? Test-flight-level rigour before going live.

## 1.7 The validation methods matrix

Methods organised by validation category × fidelity (adapted from Speero):

| Category | Low fidelity (cheap learning) | Mid fidelity | High fidelity (real-world) |
|---|---|---|---|
| **Problem & discovery** | User interviews, surveys, analytics audits | Ethnographic studies, journey mapping | n/a |
| **Concept & value prop** | Concept tests (discussion), ad creative tests, value-prop surveys | Landing page tests ("painted door"), clickable mockups | n/a |
| **Solution & experience** | Wireframe reviews, paper prototyping | Interactive prototype tests, remote usability tests | In-person usability tests, beta program |
| **Feasibility & operational** | Internal estimates, technical spikes | Internal simulations, technical prototypes | Operational pilots, data integration tests |
| **Market & business model** | Acquisition channel tests (small), pricing concept surveys | Beta launches, phased rollouts (small segment), simulated pricing | Pilot programs, larger phased rollouts, live pricing tests |
| **Optimisation & refinement** | Usability audits, analytics review | Session recording analysis, user feedback tools | A/B tests, multivariate, personalisation, funnel analysis |

A/B tests sit at the bottom right: they're the most expensive and slowest-to-learn-from option. Use them when cheaper methods can't answer the question, not as the default.

## 1.8 Matching tests to assumption types

| Assumption type | Best test types (cheap → expensive) |
|---|---|
| **Problem** | Analytics segment comparison, funnel analysis, support-ticket review, then user interviews |
| **Root cause** | Diary studies, moderated user sessions, behaviour clustering, then matched-pair analytics |
| **Desirability** | User interviews, surveys, fake-door tests, concept tests, then concierge MVP |
| **Mechanism** | Clickable prototypes, Wizard of Oz, then A/B test |
| **Magnitude** | Hard to test cheaply. Cohort projections from analogous past launches, then small-segment rollout, then full A/B |
| **Value chain** | Causal-leaning cohort analysis on existing users, matched-pair comparisons, propensity score matching |

## 1.9 Confidence ratings

For each belief and each LOFA, label the evidence level. The scale is three levels:

- **HIGH:** supported by a previous test and validated data points.
- **MEDIUM:** supported by data correlation. The rating carries the flag "correlation, not causation". The flag is part of the rating, not optional: a MEDIUM belief is one the author can name a correlation for, and has not isolated as causal.
- **LOW:** no supporting evidence yet except anecdotal or vibes.

There is no separate "None" rating. An unexamined belief is LOW with the gap named.

**Rate LOFAs on the same scale.** A low-confidence LOFA is the priority MVT target. A high-confidence LOFA is a known constraint: cite the evidence and move on rather than testing it.

**Reconciliation with the citation rule:**
- HIGH still requires a one-sentence citation naming the prior test or dataset. No citation downgrades to MEDIUM, then re-ask.
- MEDIUM means the author is claiming a correlation. Require them to name it. "Team agrees" or "behavioural psychology" with no source is not MEDIUM.
- Do not penalise a genuinely-HIGH belief for lazy shorthand. A belief can be HIGH on strong external grounds and still be written carelessly; push on the citation, not on the author's judgement.
- **Value-chain beliefs cap at MEDIUM unless the evidence is causal-leaning** (matched-pair, propensity-matched, quasi-experimental, strong analogue). A raw correlation keeps a value-chain belief at MEDIUM at best, and MEDIUM here must carry the correlation-not-causation flag.

The targets for testing are the **low-confidence, high-importance** beliefs and LOFAs. High-confidence ones can usually be left alone; low-importance ones aren't worth the test even if uncertain.

## 1.10 Tests inform decisions; they aren't decisions

A critical Longden point: a test produces evidence, not a verdict. The team takes the evidence, combines it with other inputs (qualitative research, strategic context, systems-level considerations, brand and operational risks), and makes a human decision.

This matters because it means test output should be framed as input to a decision, not "the test won, ship it." The MVT-design phase should always include a "decision criteria" section: *if X happens, we will Y; if Z happens, we will W*.

## 1.11 LOFAs: Leap of Faith Assumptions

Within an assumption list, some assumptions are "load-bearing": if they're wrong, the entire solution collapses. Borrowed from lean-startup vocabulary as **Leap of Faith Assumptions** (LOFAs). The skill keeps beliefs and LOFAs as two separate lists: beliefs are the reasoning (each with a confidence rating), LOFAs are the assumptions that kill the whole solution if wrong. The skill should explicitly identify which assumptions are LOFAs and ensure those get the most rigorous testing earliest.

### The kill-test

For each assumption, run the test:

> *"If we learned tomorrow that this assumption was wrong, what dies?"*

Three possible answers, with three different markings:

1. **The whole solution dies.** → **LOFA**. Mark with `LOFA` and prioritise testing first.
2. **One solution path dies, others survive.** → **load-bearing for that path, not the solution.** Mark with something like "load-bearing for the algorithmic route" or "gates the new-surface option". Important to test, but not a LOFA in the kill-the-solution sense.
3. **The solution survives with a minor adjustment.** → standard assumption. Test if low-confidence, leave alone if not.

### What the skill must do

- **Run the kill-test on *every* assumption.** Don't ask the user "which 1-2 of these are LOFAs?", which biases toward identifying too few. Run the test on each in turn.
- **Don't cap LOFAs at 1 or 2.** A solution with three LOFAs has three independent ways to die; the test plan needs to reflect that.
- **LOFAs often form a dependency chain.** For example, in a discovery solution: F = "is there session-length headroom?"; B = "is discovery the right lever?"; G = "does a depth lift convert to retention?". Each is independently load-bearing; the chain runs F → B → G. Write the chain order in the doc; it tells the user where the test sequence has to start.
- **Demote-when-true is allowed and important.** If a user pushes back on a LOFA designation because the solution could survive on an alternative path (e.g. editorial curation if the personalisation engine fails), demote to "load-bearing for path X" and update the test plan accordingly. This isn't the user softening the test; it's a more accurate reading of what's load-bearing.

### Common LOFA misidentifications

- **Marking only the most obvious LOFA.** Often the root-cause assumption ("is discovery the right lever?") gets missed because it sounds like background context.
- **Marking feasibility assumptions as LOFAs.** Feasibility ("can we build the engine?") is rarely a true LOFA; most engineering challenges have alternative paths. See the Cagan trap (§5.1).
- **Marking high-confidence assumptions as LOFAs.** A LOFA the team is already confident about isn't a LOFA in practice; it's a known constraint. Cite the evidence and move on.

### Shared / upstream LOFAs

Sometimes the same LOFA recurs across several problem or solution hypotheses. When that happens, testing it once, upstream, settles the whole group. This is the highest-leverage move in the framework: it stops a team running three separate tests that all secretly rest on one untested premise.

**Detection.** Scan LOFAs across *all* problem and solution hypotheses in the tree, not just within one solution, for repeats or near-repeats. A recurring LOFA reads the same way under multiple hypotheses (for example, "discovery friction is the bottleneck for this cohort" appearing verbatim under two separate problem hypotheses).

**Single upstream test.** When a LOFA recurs:
- Name it once, mark it shared, and list which solutions depend on it.
- Recommend testing it **once, upstream**, before any dependent solution is built or tested.
- Place a single stage gate on the shared-LOFA test. If it fails, every dependent solution is parked together.

On the tree diagram (Phase 5 checkpoint), draw a shared LOFA as a single node feeding the multiple solutions that depend on it.

## 1.12 Growth experiments vs optimisation

Two distinct modes (Longden):

- **Optimisation**: incremental improvement within a known framework. A/B tests on button colour, copy variants, layout tweaks. Cheap, fast, low strategic stakes.
- **Growth experiments**: validating significant, high-uncertainty strategic hypotheses. Should something new exist? Will this new proposition land? Should we change our business model?

This skill operates in the **growth experiment** mode. Optimisation work doesn't need the full theoretical-question → strategic-hypothesis decomposition; it can go straight to the solution-statement format and MVT design. The skill asks early which mode the user is in, and if it's pure optimisation, suggests the fast path.

## 1.13 The MVT (minimum viable test)

**Definition (exact):** the lowest-effort test we can run to either validate or kill a solution idea.

Not the cheapest test that informs the solution: the cheapest test that could **end** it. The kill emphasis matters. The test must have an outcome that stops the solution, not merely an outcome that is "interesting to learn from". Reject any test framed only as "would be interesting to learn from" with no failing branch. Multivariate or A/B tests can still be MVTs when there is no cheaper way to settle the assumption, or when the question is which execution path wins, not whether the premise holds.

> **DEFERRED TODO.** The full MVT blueprint (test-construct detail, fidelity-floor specifics, and sign-off mechanics) is to be fleshed out in a later pass. This section fixes the MVT definition, the kill framing, the leading/lagging/guardrail metric tiers, learning-value prioritisation, and the worked examples. Do not over-specify the blueprint mechanics now.

### Three metric tiers

An MVT names three tiers of metric, not one threshold. Require all three:

- **Leading metrics:** the proximate signals the test reads first (e.g. CTR on a unit, CTR from the unit to a full article).
- **Lagging metrics:** the downstream outcomes (e.g. average time spent per visit, average reads per visit).
- **Guardrail metrics:** what must not degrade (e.g. overall homepage CTR, visit frequency). See §1.14.

Plus a test construct (split, duration) and next-step guidance per outcome. The fidelity floor and the MVT sign-off gate are part of the deferred blueprint above.

### Learning-value prioritisation

Rank candidate MVTs by, in order:

1. **Resolves a shared LOFA** (one test kills or saves several solutions at once). Highest value.
2. Resolves a solution-specific LOFA, most upstream in the chain first.
3. Resolves a low-confidence non-LOFA that gates one solution path.
4. Informs implementation (scope/design). Deferred to a pre-build step; runs only after the gating LOFAs are green.

Keep the cheapest-first, decision-criteria, stage-gate, and fidelity-vs-cost-of-failure rules from §1.6 and §1.10.

### Is there a lower-effort test for the same point?

Always ask this before accepting a build-heavy MVT. Example: a team is about to test a personalised off-platform prompt. If the underlying beliefs are sound, the only open question is whether personalisation is the right MVT given effort. A cheaper test that proves the same point sends a single global notification about one preferred content category and reads whether it lifts CTR from the cohort. Same learning, far less build.

## 1.14 The guardrail clause

Every solution statement carries a guardrail: the metric the change must not harm, written as "Without [guardrail]". It is mandatory.

**What it catches:**
- **Cannibalisation.** A new owned-channel surface that steals visits from another, or a paid push that displaces organic return.
- **The depth-vs-frequency tradeoff.** Driving deeper sessions can suppress return frequency, or vice versa. These two axes often trade against each other (see §4.5).
- **Cohort cross-effects.** A change tuned for the light-engagement cohort that degrades the experience for core subscribers.

**How to elicit it.** If the author cannot name a metric the change might harm, push back. Most engagement changes trade against something: depth vs frequency, this cohort vs core users, owned visits vs newsletter consumption. The prompt is direct: *"What might this make worse?"* A solution with no plausible guardrail is usually a solution whose second-order effects have not been thought through.

---

# Part 2: Question and hypothesis patterns

## 2.1 Theoretical question patterns

Portfolio altitude. Skippable via Phase 0 when the user enters lower down with a direction, problem, or solution already in hand.

### Good shapes
- *"How can we [outcome] for [segment]?"*: most flexible.
- *"Why do [users] [behaviour]?"*: opens root-cause exploration.
- *"What's stopping [segment] from [behaviour]?"*: generative.
- *"How do we move [metric] from [X] to [Y] by [timeframe]?"*: when the metric is genuinely the goal, with quantification.

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

Portfolio altitude. The direction bet that selects the cohort and the project. Strategic hypotheses should be distinct, not rewordings of each other, and there should usually be 2-4. Common high-level shapes:

For **engagement** questions:
- Improve existing value (deepen what we have)
- Build new value (add new propositions)
- Change the trigger to act
- Change the default state
- Reduce friction in what already exists

Retention questions overlap but usually pull harder on value-delivery and habit-formation levers.

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

The skill should propose 3-5 strategic hypotheses appropriate to the question type, then let the user refine.

## 2.3 Problem hypothesis patterns

A problem hypothesis states that a specific, observable behaviour is broken for a named cohort, grounded in data where data exists. It names the surface or metric, not the fix. This is the level the team calls "Problem hypothesis 1". One problem hypothesis usually spawns several solution hypotheses (§2.4).

### Good shape

Data-grounded, observable, cohort-specific, names a surface or metric. Shape:

> *"For [cohort], [metric] on [surface] is markedly lower than [contrast cohort], which caps [intermediate outcome]."*

Worked good-shape example:

> *"For light-engagement subscribers of a subscription news product, article-to-article click-through is markedly lower than for core subscribers (illustrative: roughly a third of the core rate), which caps session depth."*

What makes it strong: it names the cohort, names the contrast cohort, names the surface (article-to-article), names the metric (click-through), points at data, and states the intermediate outcome it caps. It does not name a fix.

### Anti-pattern: a problem stated as a solution

The most common failure is a "problem" that is really a solution in disguise:

| Anti-pattern | Why it fails | Reframe |
|---|---|---|
| *"We need a Discover page."* | Names a fix, not a broken behaviour. Skips straight to one solution and forecloses alternatives. | *"For [cohort], content discovery on [surface] is weak: they find and open far fewer relevant items than [contrast cohort]."* |
| *"Our push notifications are underused."* | States a tool's underuse, not the user behaviour that's broken. | *"For [cohort], return frequency is low and they have few triggers to come back."* |
| *"The homepage isn't personalised."* | States a missing feature, not an observed problem. | *"For [cohort], the homepage surfaces content they don't engage with: their homepage CTR is well below [contrast cohort]."* |

The test: a problem hypothesis should be falsifiable against data and should not pre-commit to one fix. If it names the fix, it's a solution; route it to §2.4.

### Funnel decomposition (the divergence trick)

A single broken behaviour often hides several distinct causes. One low number ("this cohort clicks through on fewer items") can break at any point in a sequence the user clears in order. Decomposing it into that sequence turns one fuzzy problem into a set of isolated sub-problems, each with its own surface, metric, and candidate solutions.

The reusable move: take the broken behaviour and ask what has to go right, in order, for it not to break. For a discovery-surface click, a reader has to (1) see the item, (2) judge it worth opening, (3) want the content itself. Each stage is a causal axis:

- **See it:** placement and salience. Is the unit even in view for this cohort?
- **Judge it worth opening:** presentation and decision cues, trust and familiarity, choice load. Can the reader tell, from the card alone, that it is worth their time?
- **Want the content:** content selection and relevance. Is the right thing being surfaced at all?

Worked example, casual subscribers and session depth:

> Parent problem: for casual subscribers, click-through on the discovery surfaces is lower than for engaged subscribers, which caps session depth.
> - **See it:** recommendation units sit low in long articles; infrequent readers do not scroll far enough to see them.
> - **Judge it:** the card lacks cues (read time, format, a one-line summary) a time-poor reader needs to commit; the reader recognises fewer bylines and sections; too many or too few options cause a bounce.
> - **Want it:** the homepage is curated for core-reader topics, and the recommendation algorithm has sparse signal for infrequent users.

Two rules on using it:

1. **Build it with the user, do not invent it.** Propose the candidate axes and ask which are real for this cohort. The coach's job is to surface the space and let the user confirm what is true, not to hand over a finished six-box tree.
2. **Reach for it where the axes form a sequence.** Not every problem is a funnel. Use it when the stages genuinely gate one another (you cannot judge an item you never saw); otherwise a flat list of sub-problems is honest enough.

## 2.4 Solution patterns

A solution hypothesis is one falsifiable bet on how to fix a problem, written in the full format below. The old bare if-then-because is replaced by this richer form, which carries cohort, an explicit causal chain to the north-star, a guardrail, beliefs with inline confidence, and a separate LOFA list.

### The full-format statement

```
For [cohort]
If [X: the specific change]
Then [Y: the proximate, measurable signal, with direction]
Leading to [intermediate outcome]
Leading to [north-star metric]
Without [guardrail: the metric we must not harm]
Because we believe:
  - [belief 1]  (HIGH/MEDIUM/LOW): [evidence, or the gap that would raise it]
  - [belief 2]  (...)
LOFAs (separate list, the assumptions that kill the whole solution if wrong):
  1. [LOFA 1]
  2. [LOFA 2]
```

The operating model's terse blueprint is the floor; the full format above is the target. The terse floor reads: *"If we apply [tactical solution] then we will solve [identified problem], so [KPI] will increase. Because we believe [beliefs, each rated]. LOFAs [list, each rated]."*

Rules layered on top:
- **Y must be proximate.** The first measurable signal sits at the start of the chain (e.g. CTR on a unit), not at the north-star end (e.g. annual retention). The chain shows how Y is meant to reach the north-star; the test measures Y.
- **Each belief carries inline confidence and the evidence or the gap.** "MEDIUM: data shows the correlation, but not whether the unit is the cause" beats "MEDIUM" alone.
- **Beliefs and LOFAs are two lists.** Beliefs are the reasoning. LOFAs are decided by the kill-test (§1.11) and listed separately.
- **The guardrail is mandatory** (§1.14).
- **Specific X**: not "improve onboarding" but "personalise the first-session homepage based on declared interests".
- **Falsifiable**: there must be an observation that would prove it wrong.
- **Distinct because-clauses, usually 2-5.** One clause = one assumption. The reject is on conflation, not on count.

### Strong exemplar (obfuscated): in-article recirculation

> **Problem hypothesis: in-article recirculation**
> For light-engagement subscribers of a subscription news product, the click-through rate from one article to the next is markedly lower than for core subscribers (illustrative: roughly a third of the core rate). This caps average session depth for the cohort.
>
> **Solution hypothesis 1a: the in-article recommendation units surface the wrong content for this cohort**
>
> **For** light-engagement subscribers
> **If** we serve more relevant recommendations in the in-article units
> **Then** article-to-article click-through will increase
> **Leading to** higher average session depth
> **Leading to** higher average daily dwell time (the north-star)
> **Without** reducing visit frequency (and over the long term we expect frequency to rise, not fall)
>
> **Because we believe:**
> - The in-article units are a relatively more important discovery surface for this cohort, because the homepage is not tuned to their interests. (MEDIUM): would be stronger with data on where these users start sessions; if they land directly on articles rather than the homepage, this holds.
> - The units are not working for this cohort today: their article-to-article CTR is well below other cohorts. (MEDIUM): the CTR gap is in the data, but we have not isolated the units as the cause.
> - Article-to-article recirculation is a large driver of session depth. (MEDIUM): no cohort-specific data yet; plausible but uncited. Causal or correlational data would raise this.
>
> **LOFAs:**
> 1. Higher per-session depth will not drive visit frequency down (the depth-vs-frequency tradeoff). This is the value-chain LOFA: if depth and frequency trade off for this cohort, the north-star does not move even if the unit works.
> 2. This cohort clicks the in-article units at all. They may instead return to the homepage or follow in-body links, especially on mobile web.
>
> **MVT:** reconfigure the recommendation model for this cohort's behaviour (low build cost, no editorial input) and read article-to-article CTR against a control. Decision: if CTR rises and session depth rises without a frequency drop, progress to a wider test; if CTR rises but frequency falls, the value-chain LOFA has fired, stop and re-frame.

This carries every teaching point: a quantified problem statement, a full causal chain, beliefs each rated with an honest gap, a guardrail, and a genuine value-chain LOFA stated as a falsifiable claim.

### Solution-grouping patterns

One problem hypothesis usually spawns several solution hypotheses (1a, 1b, 1c). Keep it to 2-3 per problem, strict: more than that signals the problem isn't isolated yet.

- **How several solutions hang under one problem.** Each is an alternative bet on the same broken behaviour, not a step. Under "in-article CTR is low for this cohort": 1a serves more relevant recommendations, 1b removes units to cut decision load, 1c changes the unit's placement. The team picks the highest learning-value bet first.
- **Spotting solutions that share a LOFA.** Read the LOFA lists across all solutions under a problem (and across problems). If the same load-bearing assumption appears under more than one, mark it shared and route it to a single upstream test (§1.11). This is where the biggest time savings live: one test settles a premise that several solutions all rest on.
- **Carry build cost on each candidate.** Where solutions vary by channel or vehicle, state the rough build or infrastructure cost alongside each one as it is proposed, so the cheap-to-build path is visible during selection rather than discovered after. A candidate that reuses an existing channel (an email that houses its own content) is a different bet from one that needs a new surface built (a push that needs an on-site destination to land on), even when both attack the same problem.

---

# Part 3: Common assumption sets by solution type

These are starter sets for common solution categories. They lean toward engagement/retention product work; other domains will need their own pattern sets added over time. The skill proposes these as candidates; the user edits.

## 3.1 Discovery / findability solutions

Examples: a discovery surface, homepage personalisation, search improvements, content recommendations, cross-product discovery.

Applies to any catalogue product where users need to find something specific: content, products, listings, courses.

**Typical assumption set (run the kill-test in §1.11 on each):**
1. *(Problem)* The cohort genuinely fails to find content they'd engage with, observable in their current behaviour, not just inferred.
2. *(Root cause, often a LOFA)* The failure is due to discovery friction, not lack of time, lack of interest, substitution to other media, or content-catalogue gaps. **If this is wrong, no discovery intervention works: the lever is wrong.**
3. *(Magnitude, often a LOFA)* There is engagement headroom to capture for this cohort at all. They aren't structurally time-constrained (commute reading, snacking sessions). **If this is wrong, no discovery intervention works: there's no raw material to act on.**
4. *(Desirability)* Better-surfaced content would actually be consumed, not just seen. Stated preference for personalisation is common in industry reports; revealed preference often diverges.
5. *(Mechanism)* The proposed discovery surface or change is meaningfully better than what exists today.
6. *(Mechanism / data quality)* The personalisation infrastructure (ranking, content metadata, behavioural signal) is good enough to serve the target cohort *today*, including low-signal sub-cohorts (cold-start case).
7. *(Strategic / scope, often a LOFA when multiple surfaces are plausible)* The right surface to intervene on first. Three meaningfully different routes typically exist: (a) build a net-new surface; (b) add a new personalised component to an existing surface; (c) iterate on existing personalised surfaces (in-article rec units). They have different cost, reach, and cold-start profiles. Wrong choice here can mean a working engine and a clean theory still failing in market.
8. *(Mechanism / strategy)* The right *content mix* (narrow vs broad) is detectable and routable per session intent. Narrowing isn't a universal good; breadth-of-readership often predicts engagement.
9. *(Value chain, often a LOFA)* More content discovered → more engagement depth → improved retention metric. The depth → retention link is often *assumed* but counter-prior research (e.g. Medill / Mather "habit > intensity") suggests regularity may dominate.

**Common skipped assumptions:**
- #2 (root cause): teams treat discovery friction as obviously the explanation. It often isn't; substitution, life-stage, and structural session-length ceilings compete with it.
- #3 (magnitude / headroom): rarely tested. Without headroom, the solution dies at the source regardless of how good discovery becomes.
- #7 (strategic / scope): typically treated as an implementation detail and discovered as a problem mid-build.
- #9 (value chain): assumed by analogy to other cohorts. For low-engaged cohorts specifically, the depth → retention link can break.

**Default cheap test designs for discovery solutions:**

| Assumption tested | Cheap test | Where it fits in the chain |
|---|---|---|
| Magnitude / headroom (#3) | **Engagement-spike trigger and trajectory analysis.** Identify light-engagement subscribers who had a sustained engagement spike. Classify the trigger (controllable vs exogenous), then matched-pair against a non-spike cohort to check whether the spike sustained and converted to weekly visits and retention. | Tests headroom (#3) directly; partially tests value chain (#9) via the trajectory cut. The most efficient single retrospective. |
| Root cause (#2) | **Discovery-path engagement comparison.** Within the target cohort, compare session depth across entry paths: curated paths (homepage, channel index) vs bypass paths (search, push, newsletter, direct). If bypass-path users engage materially more deeply, curation is plausibly the friction. Match on tenure and persona to reduce selection bias. | Tests root cause (#2). Caveat: residual selection effects; treat alongside spike-trigger analysis, not as a verdict. |
| Mechanism / data quality (#6) | **Offline personalisation eval** on the target cohort's history if infrastructure allows. Otherwise: **historical analysis of a previous personalised surface** (e.g. a homepage "for you" trial) segmented by engagement cohort. If neither available, a **small in-product CTR probe** comparing engine output to editorial baseline. | Tests engine quality for the cohort, separate from whether discovery is the right lever. Cheaper retrospectives first. |
| Mechanism / strategy (#8) | **In-article recommendation performance by topic and entry channel.** Check whether narrow-vs-broad has a clean pattern by topic or by inferred session intent. Implementation-design work; runs *after* the gating LOFAs are resolved. | Pre-build, not gating. Informs the design of whatever gets built in the full test. |
| Strategic / scope (#7) | Use the historical-surface retrospectives as triangulation: *(a)* a prior new-surface attempt (a prior standalone personalised surface) informs route (a); *(b)* a prior personalised-component-on-existing-surface trial informs route (b); *(c)* aggregate performance of existing personalised slots informs route (c). The strongest signal of the three informs which route to build first. | Resolved at the stage gate after the LOFA tests. |

The whole pattern: spike analysis + path comparison cover the two cheapest LOFA tests. Combined with one historical-surface retrospective per available route, they form the standard Wave 1 of a discovery-solution test plan.

## 3.2 On-content engagement solutions

Examples: adaptive article layouts, new storytelling formats, TL;DR boxes, audio versions, in-article features.

Scopes specifically to the in-session experience once the user has arrived at the thing.

**Typical assumption set:**
1. *(Problem)* The cohort is arriving at content but disengaging before getting value.
2. *(Root cause)* The on-page experience is what's causing disengagement (not headline mismatch, not device context, not topic disinterest).
3. *(Root cause)* This cohort has on-page needs distinct from engaged users.
4. *(Mechanism)* The proposed intervention addresses the actual friction point.
5. *(Magnitude)* The proximate metric we'd move (scroll depth, completion rate) is sensitive enough to detect a real change.
6. *(Value chain)* The proximate metric correlates with the business metric.

**Common skipped assumption:** #2. Teams design article-level interventions when the disengagement happens at headline-click or context-mismatch level.

## 3.3 Off-platform return-mechanism solutions

Examples: newsletter sign-ups, push notifications, re-engagement email in SaaS, transactional comms in commerce, podcast or social presence.

**Typical assumption set:**
1. *(Value chain, usually the LOFA)* The touchpoint causally drives return visits, not just correlates with them. Selection bias is huge here.
2. *(Problem)* The cohort isn't sufficiently exposed to or signed up for the touchpoint.
3. *(Desirability)* The cohort will sign up when given better placement/defaults.
4. *(Desirability)* Once signed up, the cohort will actually engage with the touchpoint (open rate × CTR).
5. *(Mechanism)* The proposed sign-up surface materially outperforms current.
6. *(Magnitude)* The new sign-ups translate into measurable return-visit lift at cohort level.

**Common skipped assumption:** #1. Almost universal in product teams. The skill should aggressively flag this.

**Obfuscated weak example (push opt-in):**

> *If we get light-engagement subscribers to opt in to recommended notifications, then they will be alerted to relevant stories, leading to higher visit frequency. Because we believe: push is a highly effective frequency lever; many of the cohort are opted out.*

This fails several gates at once: no proximate signal (Y jumps to frequency), generic LOFAs, no guardrail. Two specific belief problems recur in this solution type and are worth flagging by name:

- **Vague belief.** "Previous tests showed a positive improvement to engagement when notifications were activated." Improvement in what? Frequency or session depth? A belief citing a prior result must name the metric and direction.
- **Belief disconnected from the mechanism.** "Research indicates light-engagement subscribers value lifestyle and culture content but feel overwhelmed by a breaking-news-dominated experience." True, perhaps, but it does not explain how *personalised push* acts on it. Route it to the value-chain gate.

The sharper fix is upstream: if low push CTR is actually a sign-up/opt-in problem rather than a relevance problem, the first test isn't to personalise the notifications, it's to test the messaging and the sign-up surfaces. A sharp problem hypothesis the step before would have isolated the CTR problem specifically. And before building personalised push at all, ask whether a lower-effort test proves the same point (§1.13): send a global notification about one preferred content category and read the cohort's CTR.

## 3.4 New value proposition solutions

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

## 3.5 Onboarding / activation solutions

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

These show the framework in action across different domains. The point of having more than one is to show that the same spine applies whether the question is about content engagement, fitness activation, or B2B SaaS.

## 4.1 Flagship: in-article recirculation (full format, end to end)

This is the model for the new format. It carries a quantified problem statement, a full causal chain to the north-star, beliefs each rated with an honest gap, a guardrail, and a genuine value-chain LOFA.

> **Problem hypothesis: in-article recirculation**
> For light-engagement subscribers of a subscription news product, the click-through rate from one article to the next is markedly lower than for core subscribers (illustrative: roughly a third of the core rate). This caps average session depth for the cohort.
>
> **Solution hypothesis 1a: the in-article recommendation units surface the wrong content for this cohort**
>
> **For** light-engagement subscribers
> **If** we serve more relevant recommendations in the in-article units
> **Then** article-to-article click-through will increase
> **Leading to** higher average session depth
> **Leading to** higher average daily dwell time (the north-star)
> **Without** reducing visit frequency (and over the long term we expect frequency to rise, not fall)
>
> **Because we believe:**
> - The in-article units are a relatively more important discovery surface for this cohort, because the homepage is not tuned to their interests. (MEDIUM): would be stronger with data on where these users start sessions; if they land directly on articles rather than the homepage, this holds.
> - The units are not working for this cohort today: their article-to-article CTR is well below other cohorts. (MEDIUM): the CTR gap is in the data, but we have not isolated the units as the cause.
> - Article-to-article recirculation is a large driver of session depth. (MEDIUM): no cohort-specific data yet; plausible but uncited. Causal or correlational data would raise this.
>
> **LOFAs:**
> 1. Higher per-session depth will not drive visit frequency down (the depth-vs-frequency tradeoff). This is the value-chain LOFA: if depth and frequency trade off for this cohort, the north-star does not move even if the unit works.
> 2. This cohort clicks the in-article units at all. They may instead return to the homepage or follow in-body links, especially on mobile web.
>
> **MVT:** reconfigure the recommendation model for this cohort's behaviour (low build cost, no editorial input) and read article-to-article CTR against a control. Decision: if CTR rises and session depth rises without a frequency drop, progress to a wider test; if CTR rises but frequency falls, the value-chain LOFA has fired, stop and re-frame.

## 4.2 MVT worked example: remove the units for a week

This teaches the core MVT move: test the premise by subtraction, not by building the polished solution.

> A team's solution designs all rest on one principle: offering fewer recommendations to cut decision fatigue. The evidence points that way and the concepts tested well in usability sessions. But there is no hard evidence for the decision-fatigue premise itself, the crux of the whole solution. Building multivariate personalised-list experiences is a high-effort way to learn that the premise was wrong. So the MVT is to **remove the two in-article recommendation units for this cohort for one week**, and agree up front that if engagement does not move, any solution resting on the decision-fatigue premise stops there. One cheap, reversible subtraction tests the load-bearing belief before any build.

Why it works: the decision-fatigue premise is a shared LOFA under every solution in the set. One subtraction either kills all of them or clears them. It is reversible, costs almost nothing, and has a failing branch agreed in advance. That is an MVT, not a "would be interesting to learn from" test.

## 4.3 Worked example: Activating new sign-ups in a fitness app

The team wants more new sign-ups to complete their first workout in week one.

**Theoretical question:** *How can we get more new sign-ups to complete their first workout in week one?*

**Strategic hypothesis A:** *By reducing the effort to start the first workout.*
- *Shorten the in-app warm-up*
- *Pre-select a starter programme based on sign-up answers*
- *Surface a 10-minute "any day" option as the default*

**Strategic hypothesis B:** *By raising motivation in the first 72 hours.*
- *Send a single nudge timed to the user's declared weekday slot*
- *Pair new users with a human coach for one check-in*
- *Show a peer-group progress view*

**Strategic hypothesis C:** *By making the first workout pre-committed rather than opt-in.*
- *Schedule the first session at sign-up and send a calendar invite*
- *Link the session to an existing routine (post-coffee, lunch break)*
- *Add a social commitment: invite a friend, share the goal publicly*

The three sit at the same altitude. They're alternatives, not steps; the team will pick one direction to invest in first.

Candidate MVTs span the validation matrix: a moderated session to understand pre-first-workout drop-off (root-cause), a painted-door landing test for the human-coach offer (desirability), and a small-segment A/B on starter-programme pre-selection (mechanism + magnitude). Each test addresses assumptions specific to its parent solution, not "does the activation strategy work?"

## 4.4 Worked example: Lifting weekly return rate in a SaaS product

A B2B SaaS team wants to raise weekly active use among admins on the standard tier who only log in once a fortnight.

**Theoretical question:** *How can we increase weekly active rate among standard-tier admins?*

**Strategic hypothesis A:** *By improving mechanisms that bring them back.*
- *Improve the weekly digest email*
- *Add an in-product notification for actionable events*
- *Make the dashboard the default landing page on return*

**Strategic hypothesis B:** *By giving them weekly reasons to come, or removing the reasons not to.*
- *Move a key workflow from monthly to weekly cadence*
- *Surface fresh data they currently only see on demand*
- *Cut the friction of getting back in (SSO, longer session, recognised device)*

Two notes:

1. A and B are alternative bets, not steps. The team picks one direction to invest in first.
2. B's solutions imply different things about whether the product currently has a weekly use case at all. If it doesn't, that's a more upstream question than this tree assumes.

## 4.5 Frequency vs depth in content products

Engagement in content/subscription products usually decomposes into two largely orthogonal axes:

- **Frequency**: how often does the user return?
- **Depth**: how much do they engage in each visit?

Strategic hypotheses cluster differently for each. Frequency-side hypotheses are usually about touchpoints, habits, and reasons to return (off-platform mechanisms, push, newsletters, exclusive content). Depth-side hypotheses are usually about value, discovery, and on-content experience.

The two axes often trade against each other, which is why the guardrail clause (§1.14) exists. Driving deeper sessions can suppress return frequency; driving frequency can fragment sessions. When a solution moves one axis, name the other as the guardrail.

Frequency and depth show up in content products especially clearly, but the same split applies in SaaS (return cadence vs depth of session), marketplaces (return-buy rate vs basket size) and others.

When a user presents a theoretical question that mixes the two, the skill should ask them to split it; they need different hypotheses and different metrics.

---

# Part 5: Anti-patterns and traps

The skill should watch for these and flag them to the user.

## 5.1 The feasibility over-index (Cagan)

Teams systematically pick assumptions and tests engineers are comfortable with: technical spikes, prototypes, build-and-A/B-test. They under-invest in value and viability questions, which are scarier and harder. If a user's assumption list has zero desirability or value-chain assumptions, push back hard.

**Canonical fixture (obfuscated): the single feasibility because-clause.**

> *We believe targeted display ads will pull dormant light-engagement subscribers back. Because we believe: we can reach users further than our traditional channels. [No value, desirability, or value-chain reasoning.]*

The sole because-clause is a reach-and-feasibility claim ("we can reach users"). It says nothing about whether the cohort wants what the ad offers (desirability), whether reaching them moves the metric (value chain), or what the ad even surfaces (value). A solution justified only by "we can reach/build/do X" is the Cagan trap in one line. Reject it and route the author back to value and value-chain reasoning.

## 5.2 Metric thinking vs systems thinking (Longden)

Picking the highest-projected-impact initiative without considering systems effects. Classic case: a deep discount campaign lifts quarterly revenue but suppresses full-price conversion for the following two quarters as customers learn to wait for promotions.

When a user proposes a solution, ask: *what are the second-order effects? What might this break elsewhere? What's the downstream impact on other metrics or brand?* If the answer is "I haven't thought about it," that's a value-chain assumption gap and usually a missing guardrail (§1.14).

## 5.3 Sense-checking vs experimenting (Longden)

"We A/B tested the feature when we shipped it" is not experimentation; it's sense-checking. By the time the feature is built, the assumptions baked in are already mostly determined. Real experimentation happens before the build, testing the assumptions that justify the build.

The skill enforces this by requiring assumption-level testing before solution design.

## 5.4 "Vibes-based" prioritisation

Solutions get prioritised by gut-feel and presentation polish rather than evidence. The pushback rules require explicit confidence ratings and evidence citations; this exists to disrupt vibes-based prioritisation. When a user rates a belief "HIGH confidence" with no evidence cited, the skill should challenge: *what's the evidence?*

## 5.5 "Ship and pray"

Building the full feature, releasing, watching metrics, hoping. The horse-race ladder exists to prevent this. The skill should always propose the cheapest test first, even when the user wants to skip to "let's just build it." Cost-of-failure framing helps: *if this is wrong and we ship it, what does it cost to roll back, and what's the brand/customer impact?*

## 5.6 A/B testing as innovation

A/B tests are an optimisation tool, not an innovation tool. They tell you which of two variants is better within a known framework. They don't tell you whether you should be in that framework at all. For genuinely novel propositions, A/B testing is the wrong method: you need qualitative validation first, then concept tests, then prototype tests, then A/B as the final check.

## 5.7 Mistaking correlation for causation in value-chain assumptions

"Users who enable notifications retain at far higher rates than those who don't." Almost certainly inflated by selection bias: people who enable were already going to retain more. The skill should always require causal-leaning evidence (matched-pair, propensity-matched, or quasi-experimental) for value-chain assumptions, not raw correlations. This is the same cap that holds value-chain beliefs at MEDIUM in §1.9.

## 5.8 The shared untested LOFA

Several solutions, each tested separately, all secretly rest on one untested premise. The team burns three test cycles when one upstream test would have settled the lot.

**Fixture (obfuscated):**

> *The LOFA "discovery friction is the bottleneck for this cohort" appears verbatim under two problem hypotheses, untested. Route to one upstream test before any dependent solution.*

Detection and the fix are in §1.11 (shared / upstream LOFAs): scan LOFA lists across the whole tree, name the recurring one once, mark it shared, and place a single stage gate on one upstream test. If it fails, every dependent solution is parked together. This is the highest-leverage check in the framework.

---

## Notes for future iteration

- Flesh out the full MVT blueprint (test-construct detail, fidelity-floor specifics, sign-off mechanics), currently deferred (§1.13).
- Add patterns for paid/monetisation solutions when relevant.
- Add patterns for B2B/enterprise products.
- Add patterns for e-commerce, marketplace, and platform products.
- Consider adding a section on cohort segmentation methods.
- Build a library of real completed-test cases as the skill is used.
- Speero's UX heuristics (Value, Relevance, Clarity, Friction, Motivation) could become a structured prompt for generating solutions under "improve existing on-platform value" strategic hypotheses.
