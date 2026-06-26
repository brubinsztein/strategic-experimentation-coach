# Strategic Experimentation Skill: Pushback Rules

**Version:** 1.0
**Status:** Live rulebook, iterate as the skill is used
**Purpose:** Codifies what the skill rejects, why, and how, at each phase of the conversation. The skill's pushback is its core value. Without it, the skill is just a structured Q&A; with it, the skill enforces the discipline that PMs typically skip.

---

## How to use this document

This is a living rulebook. As the skill is used:

- If a PM-team conversation surfaces a category of weak input not covered here, add it.
- If a reject criterion is firing too often on legitimate inputs, soften it.
- If a reject criterion is *not* firing when it should, sharpen it.

Each phase below lists: the criteria, what the skill says when triggered, and worked examples of good vs. bad inputs. Named reject criteria (GUARD-1, CHAIN-1, VC-GATE-1, BELIEF-LINK, VAGUE-METRIC, PROBLEM-ISOLATES, SHARED-1, FEAS-BECAUSE, KILL-1, LOWER-EFFORT-MVT) carry stable IDs so SKILL.md and the pattern library can reference them.

---

## Changelog

- **v1.0**, Re-based onto the full six-level spine (theoretical question → strategic hypothesis → problem hypothesis → solution hypothesis → MVT → validated/production solution). Re-numbered phases (0 triage, 1 theoretical question, 2 strategic hypotheses, 3 problem hypotheses, 4 solution hypotheses + prioritise, 5 checkpoint, 6a/6b/6c deep-dive, 7 MVT design, 8 handoff), absorbed the old functional-hypothesis (tactic) layer into the problem hypothesis, added ten named reject criteria, split the assumption output into beliefs and LOFAs, replaced the source-count confidence scale with HIGH/MEDIUM/LOW, promoted the value-chain connection to a first-class gate, and added the passable-vs-better worked pushback rule.
- **v0.2**, Loosened Phase 5a rules on magnitude and because-clause count. Added a sixth core principle on precision. Removed em dashes throughout.
- **v0.1 (initial)**, drafted from synthesis of Cagan, Torres, Bland, Gilad, and Longden/Speero frameworks.

---

## Core principles

1. **Pushback is in service of the PM's success, not skill stubbornness.** Every rejection must explain why and offer reframes. Never reject without giving the PM a way forward.
2. **Aggressive on the discipline, generous on the assumptions about the PM.** Assume the PM is smart, busy, and would do this right if they had the time. Don't lecture.
3. **The skill is not the decider.** PMs can override any pushback with a stated reason. Log the override; don't refuse to proceed.
4. **Sanity checks beat exhaustive checks.** It's better to surface one critical issue clearly than five marginal issues exhaustively.
5. **Show, don't tell.** When rejecting, propose 2-3 specific reframes rather than abstract principles.
6. **Precision where it earns its keep.** Insist on falsifiability and distinctness. Don't insist on numeric magnitudes the team has no basis for, or a fixed count of because-clauses. Made-up precision is worse than honest 'we don't know yet'.

## Pushback delivery style

When the skill detects a reject criterion firing, it should:

1. **Name the issue specifically.** Not "this isn't quite right" but "this names a solution rather than a question."
2. **Explain why it matters in one sentence.** Why does this distinction affect the work downstream?
3. **Offer 2-3 reframes**, drawn from `pattern-library.md` where possible.
4. **Ask the PM to choose, edit, or override.**

**Example of good pushback delivery:**

> *"'Should we build a Discover page?' names a solution rather than a question, which constrains us to that one direction before we've explored whether discovery is actually the right lever. A few reframes:*
> - *'How can we make content easier for light-engagement subscribers to discover?'*
> - *'Why do light-engagement subscribers fail to find content they'd enjoy?'*
> - *'What's stopping light-engagement subscribers from engaging more deeply?'*
> *Want to go with one of these, edit, or stick with the original?"*

**Example of bad pushback delivery:**

> *"Your theoretical question doesn't conform to the patterns in this framework. Please revise it to be outcome-focused and to admit multiple solution directions."*

(Why bad: abstract, doesn't say what's wrong, doesn't give the PM anything to work with.)

---

## Phase 0, Entry triage

No real pushback here, just routing. The skill asks where the PM is starting and routes to the right altitude:

- vague portfolio goal → Phase 1 (theoretical question)
- has a direction → Phase 2 (strategic hypotheses)
- has a project or problem → Phase 3 (problem hypotheses)
- has a solution → Phase 6a (solution-hypothesis format) then Phase 7 (MVT)
- pure optimisation → fast path (6a + 7)

**One soft check:** if the PM says "I have a solution, just help me design the test," the skill should ask: *"Quick check: do you have a full-format hypothesis statement for it, with beliefs and LOFAs identified? If not, we should do that first; MVT design without it tends to test the wrong thing."* This is the only escape hatch with a guard rail on it.

---

## Phase 1, Theoretical question (portfolio altitude)

The high-level question that frames the investment area and sets the metric family. Skippable via Phase 0 when the PM enters lower down.

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **Must be a question, not a statement** | *"How can we increase engagement among light-engagement subscribers?"* | *"We need to increase engagement among light-engagement subscribers."* |
| 2 | **Must be outcome-focused, not solution-focused** | *"How can we make content easier for light-engagement subscribers to discover?"* | *"Should we build a Discover page?"* |
| 3 | **Must not be yes/no** | *"What would happen if we changed our free tier?"* | *"Should we cut the free tier?"* |
| 4 | **Must not be a pure metric target** (it can reference a metric, but not be one) | *"How can we grow our active user base among [cohort]?"* | *"How do we get to 1M DAU?"* |
| 5 | **Must be narrow enough to be tractable** | *"How do we grow [cohort] over [timeframe]?"* | *"How do we grow?"* |
| 6 | **Must not conflate multiple questions** | Pick one of two | *"How do we acquire younger users and retain them better?"* |
| 7 | **Must be about outcomes, not outputs** | *"How do we increase engagement?"* | *"How do we ship more features?"* |
| 8 | **Should specify a cohort or segment where relevant** | *"...among light-engagement subscribers"* | *"...among users"* (when the team isn't actually trying to move everyone) |

### Soft check (not a reject, but flag)

- **Frequency vs depth conflation in engagement questions.** If the PM's question covers both ("how do we increase engagement"), the skill should ask: *do you mean frequency, depth, or both? They have different hypotheses and metrics, worth splitting unless you have reason to keep them together.*

---

## Phase 2, Strategic hypotheses (portfolio altitude)

The direction bet that selects the cohort and the project. Skippable via Phase 0 when the PM already has a project or problem. Gate on confidence before descending.

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **Must be at least 2 distinct hypotheses** | Two genuinely different directions | One direction with rephrasings |
| 2 | **Must be at the right altitude (direction, not lever or solution)** | *"By improving existing value propositions"* | *"By adding a Discover page"* (solution) or *"By making the homepage better"* (too narrow) |
| 3 | **Must plausibly answer the theoretical question** | *(Strategic hypotheses for an engagement question)* about value, reach, friction, etc. | *(For an engagement question)* "By acquiring more users" (wrong question) |
| 4 | **Must be meaningfully distinct from each other** | A: "Improve existing value" / B: "Build new value" / C: "Change who we target" | A: "Make content better" / B: "Improve content quality" |
| 5 | **Should not all be on one dimension** | Mix of internal-product and external-touchpoint bets | All four about internal product changes (misses off-platform options) |

### Soft check

- **Are contradictory hypotheses present?** This is *good* at the strategic-hypothesis level. If all hypotheses align in the same direction, the PM may not have considered alternative bets. Prompt: *"What's the bet you're not considering? Strong strategic maps usually include at least one option that contradicts another. They're alternatives to choose between, not steps in a sequence."*

---

## Phase 3, Problem hypotheses

Elicit 1-4 problem hypotheses. Each names a broken, observable behaviour for the cohort, grounded in data where data exists, and names a surface or metric, not a fix. The old functional-hypothesis (tactic) layer is absorbed here.

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **Must name a broken behaviour, not a fix** | *"Article-to-article click-through is markedly lower for light-engagement subscribers than for core subscribers."* | *"We need a Discover page."* (a solution wearing a problem's clothes) |
| 2 | **Must be cohort-specific** | Names the cohort and a contrast cohort | *"Engagement is low"* (whose?) |
| 3 | **Must be grounded in data where data exists**, naming the surface or metric | *"On the in-article recommendation unit, CTR for this cohort is well below other cohorts."* | An unevidenced assertion with no metric or surface named |
| **PROBLEM-ISOLATES** | **Must isolate the issue, so the first solution test attacks the right thing.** If the problem is left unisolated (e.g. opt-ins conflated with CTR), the first MVT may be the wrong test. Tied to the passable-vs-better critique (see end of doc). | *"CTR from the prompt is low for this cohort"* (isolated) | *"Engagement from the prompt is weak"* (could be a sign-up problem or a CTR problem; the next phase can't tell which to test) |

### Soft check

- **Coverage check.** Across the problem hypotheses in this branch, are the obvious broken behaviours covered? Compare to `pattern-library.md` and flag a missing one without insisting it be added.

---

## Phase 4, Solution hypotheses and prioritisation

For each problem hypothesis, propose 2-3 solution hypotheses (strict; do not over-commit). Group solutions that share a LOFA. Prioritise problems and solutions by importance, confidence, speed-to-learn, and shared-assumption coverage.

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **Must be concrete and falsifiable** | A named change to a named surface for the cohort | *"Improve discovery"* |
| 2 | **Must ladder up to its parent problem hypothesis** | The solution is recognisably a way to fix that problem | The solution could sit under any problem |
| 3 | **At most 2-3 per problem** | A small, distinct set | A long feature list in disguise |
| 4 | **Solutions sharing a LOFA must be grouped** | The group is named, with the shared LOFA flagged (routes to SHARED-1 in 6b) | Three solutions tested separately, each secretly resting on the same untested premise |
| 5 | **Prioritisation must weigh shared-assumption coverage** | A solution whose test also resolves a shared LOFA ranks up | Ranking by gut feel or build order alone |

### Soft check

- **Speed-to-learn.** Where two solutions are close on importance and confidence, prefer the one whose MVT settles faster. Flag this, don't force it.

---

## Phase 5, Checkpoint

Present the tree: Theoretical question → Strategic → Problem → Solution(s) → MVT. Priority styling unchanged.

### Soft check

- **Mark shared LOFAs on the diagram.** Draw any LOFA that feeds more than one solution as a single node feeding those solutions. This is the visual cue for the SHARED-1 routing in Phase 6b.
- **Revise loop.** If the tree exposes a problem hypothesis that no solution genuinely attacks, route back to Phase 3 rather than forcing a solution onto it.

---

## Phase 6a, Full-format statement

Each priority solution is restated in the full format:

```
For [cohort]
If [X: the specific change]
Then [Y: the proximate, measurable signal, with direction]
Leading to [intermediate outcome]
Leading to [north-star metric]
Without [guardrail: the metric we must not harm]
Because we believe:
  - [belief]  (HIGH/MEDIUM/LOW): [evidence, or the gap that would raise it]
LOFAs (separate list): ...
```

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **X must be specific** | *"Reconfigure the in-article recommendation units to serve more relevant content for this cohort"* | *"Improve discovery"* |
| 2 | **Y must be measurable with direction. Add magnitude only when there's grounds for one** | *"Article-to-article click-through will rise materially in this cohort over 6 weeks (when anchored in baseline data); or ...rise by a stated amount; magnitude TBD pending baseline"* | *"...engagement will go up"* (no direction); or a precise figure with no analogue or baseline to anchor it |
| 3 | **Y must be a proximate metric** that could plausibly move on the test's timescale | CTR on the unit, articles per session, return rate over 4 weeks | LTV, annual retention (too downstream for a single test) |
| 4 | **Because-clauses must be distinct and falsifiable** | Each belief separately testable | One conflated clause; or *"because it would be better"* |
| 5 | **Because-clauses must not be solutions in disguise** | *"...because discovery friction is the binding constraint"* | *"...because users want a Discover page"* |
| 6 | **Must specify the cohort** | *"For light-engagement subscribers"* | *"For users"* |
| **CHAIN-1** | **Must state the causal chain to the north-star via named intermediate steps, and Y must be the proximate signal, not the north-star.** | *"Then CTR rises → leading to higher session depth → leading to higher daily dwell time"* | A statement that jumps "prompts → return frequency → dwell time" with no proximate measurable signal at the front of the chain |
| **GUARD-1** | **Must include a guardrail clause.** Distinguish two cases. **Missing guardrail (reject):** the author names no metric the change might harm; push back, since engagement changes usually trade against depth, frequency, another cohort, or owned-channel consumption. **Misplaced guardrail (relocate, don't reject):** guardrail thinking is present but sits in the success or "we will know" line rather than the `Without` clause; acknowledge it and push the author to move it into the `Without` clause so the tradeoff is stated where the format expects it. | *"Without reducing visit frequency"* in the `Without` clause | No guardrail anywhere, or a guardrail stated only in the success line (e.g. *"without increasing unsubscribes"* tucked into the "we will know" sentence) |
| **BELIEF-LINK** | **Each belief must connect to the solution mechanism.** Reject a belief that states a user truth but never explains how *this* change acts on it. | *"The in-article units are this cohort's main discovery surface, because the homepage isn't tuned to their interests, so re-ranking them is what moves their CTR."* | *"Research indicates light-engagement subscribers value their preferred content categories but feel overwhelmed by breaking-news-dominated experiences"*: true, but doesn't say how it links to the solution. Route to the value-chain gate. |
| **VAGUE-METRIC** | **A belief citing a prior result must name the metric and direction.** "Previous tests showed improvement" is rejected: improvement in what? | *"A prior test lifted return frequency for this cohort"* | *"Previous tests showed a positive improvement to engagement when notifications were activated"*: was this frequency or session depth? Be specific. |
| **inline confidence** | **Each belief carries its confidence and evidence (or the gap) inline**, not in a separate ratings pass. | *"MEDIUM: the data shows the correlation, but not whether the unit is the cause."* | A bare belief with no rating, or *"MEDIUM"* with no evidence and no gap |

**PROBLEM-ISOLATES** also fires here when a solution's first test would attack an unisolated problem (see Phase 3). **FEAS-BECAUSE** spans 6a/6b (see Phase 6b).

### Soft check

- **Made-up precision.** If the magnitude has no anchoring evidence (analogue, prior test, baseline), prefer 'TBD pending baseline' over an invented number. Fabricated thresholds anchor decisions later and read as false confidence.

---

## Phase 6b, Beliefs and LOFAs

Keep the kill-test as the method. Output **two lists**: beliefs (the reasoning, each with confidence) and LOFAs (the load-bearing assumptions that kill the whole solution if wrong, each rated).

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **Two separate lists** | Beliefs listed as reasoning; LOFAs listed separately, decided by the kill-test | One undifferentiated assumption list |
| 2 | **At least one root-cause and one value-chain assumption present** | *"The drop-off is because of X"* plus *"the proximate metric reaches the north-star"* | All assumptions about the immediate intervention |
| 3 | **Must not all be of one type** | Mix of problem, root-cause, desirability, mechanism, magnitude, value-chain | All desirability, or all mechanism |
| 4 | **Kill-test on every assumption, not "pick 1-2"** | Each assumption run through the kill-test; however many genuine LOFAs the solution has are marked | "Pick the 1-2 most important": biases toward too few |
| 5 | **Not all feasibility-flavoured** (Cagan trap) | Mix of risk types | All about whether engineering can build it |
| **VC-GATE-1** | **Value-chain gate (first-class).** Every solution must contain at least one *stated, mechanism-linked* belief or LOFA that explains **why** moving the proximate metric moves the north-star, written as a falsifiable claim. An item merely present in a list does not clear the gate; the claim must spell out the causal link. Two failure modes the gate must catch: (a) a solution that also fails FEAS-BECAUSE can still bury a value-chain LOFA in the list, and (b) a value-chain claim resting only on a raw correlation (MEDIUM-capped per `pattern-library.md` 1.9 and 5.7) cannot be the sole gate-satisfier. If the only value-chain reasoning is a raw correlation, the gate is not cleared: the coach flags it and routes the causal link to an MVT. | *"Higher per-session depth will not drive visit frequency down (the depth-vs-frequency tradeoff)"* stated as a LOFA, with the mechanism named | A set of beliefs about the cohort's problems with nothing connecting them to visit depth or frequency; or a lone *"opted-in users return more often"* raw correlation offered as the value-chain claim |
| **SHARED-1** | **Shared-LOFA flag.** If a LOFA appears under more than one hypothesis, mark it shared and route it to a single upstream test before any dependent solution is built. | *"'Discovery friction is the bottleneck for this cohort' is the LOFA under two problem hypotheses; test once, upstream."* | The same LOFA tested three times inside three separate solution tests |
| **FEAS-BECAUSE** | **A single feasibility-flavoured because-clause is a reject (the Cagan trap, sharpened).** A solution justified only by "we can reach/build/do X" has no value or value-chain reasoning. | At least one value and one value-chain belief alongside any feasibility point | *"We believe targeted display ads will pull dormant light-engagement subscribers back. Because we believe: we can reach users further than our traditional channels."* (no value, desirability, or value-chain reasoning) |

### Soft check

- **Cross-reference the solution type.** If the solution is an off-platform touchpoint, does the LOFA list include the value-chain LOFA that the touchpoint causally drives return visits (not just correlates)? This is the most commonly skipped assumption in this category. See `pattern-library.md` 3.3.
- **Discovery / findability solutions** should include both the headroom (magnitude) LOFA and the surface-choice (strategic / scope) LOFA. See `pattern-library.md` 3.1.
- **The LOFA chain.** When multiple LOFAs are identified, ask: do they form a dependency chain (if upstream fails, downstream is moot)? Writing the chain order tells the team where the test sequence must start.
- **Lone feasibility belief among value beliefs.** FEAS-BECAUSE only fires on a *sole* feasibility because-clause, and reject criterion 5 only fires when *all* beliefs are feasibility-flavoured. A single feasibility belief sitting among genuine value beliefs slips through both. Flag any feasibility-flavoured belief that does no value or value-chain work, even when the other beliefs are sound, and ask whether it earns its place. Example: *"This approach sidesteps the personalisation infrastructure challenge"* alongside three real value beliefs, it is true but carries no value-chain weight.

---

## Phase 6c, Confidence ratings

Each belief and each LOFA carries an inline rating on the HIGH/MEDIUM/LOW scale:

- **HIGH:** supported by a previous test and validated data points.
- **MEDIUM:** supported by a data correlation, flagged as correlation-not-causation. The flag is part of the rating, not optional.
- **LOW:** no supporting evidence yet except anecdotal/vibes.

LOFAs are rated on the same scale. A low-confidence LOFA is the priority MVT target; a high-confidence LOFA is a known constraint.

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **HIGH must cite the prior test or dataset in one sentence** | *"HIGH: the Q3 funnel test lifted this cohort's CTR, validated against held-out data."* | *"HIGH: we just know"* |
| 2 | **No-citation = downgrade.** No one-sentence source → HIGH drops to MEDIUM, then re-ask. | The skill enforces this every time. | Letting an uncited HIGH ride. |
| 3 | **MEDIUM means a named correlation, flagged not-causation** | *"MEDIUM: the data shows the CTR gap, but we have not isolated the unit as the cause."* | *"MEDIUM: feels about right"* with no correlation named |
| 4 | **"Team agrees" is not evidence** | Cite data, research, or an analogous case | *"HIGH: the team is aligned"* / *"MEDIUM: the team thinks so"* |
| 5 | **Value-chain beliefs cap at MEDIUM unless the evidence is causal-leaning** (matched-pair, propensity-matched, quasi-experimental, strong analogue). A raw correlation keeps them at MEDIUM, carrying the correlation-not-causation flag. | *"MEDIUM: correlation only; a matched-pair read would raise it"* | HIGH on a value-chain belief backed by raw correlation |
| 6 | **Don't penalise a genuinely-HIGH belief for lazy shorthand.** A belief can be HIGH on strong external grounds and still be written badly. Push on the citation, not on the author's judgement. | *"You've got the grounds; just name the prior test or dataset so it reads as HIGH."* | Downgrading a sound belief because the wording was terse |
| 7 | **A low-confidence LOFA must have an MVT proposed** | Skill carries it to Phase 7 as the priority target | Marked LOW but no test planned |
| 8 | **Watch for ratings that contradict earlier statements.** If the author earlier flagged an assumption as a known weakness then rates it MEDIUM without explanation, pause and ask what changed. | *"You flagged this as a concern; rating it MEDIUM now means resolved, or 'works for core but uncertain for this cohort'?"* | Letting a flagged concern silently become "MEDIUM = fine". |

### Soft check

- **Distribution check.** If the author rates the large majority of beliefs HIGH, ask: *"That's a lot of high-confidence beliefs for new work. Which is the one you're least sure about?"* A gentle nudge, not a hard reject.

---

## Phase 7, MVT design

An MVT is the lowest-effort test that can validate or **kill** a solution. Rank MVTs by learning value: resolves a shared LOFA first (kills or saves several solutions at once), then a solution-specific LOFA most upstream in the chain, then a low-confidence non-LOFA that gates one path, then implementation work (deferred to pre-build).

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| **KILL-1** | **The MVT must be able to kill the solution, not only confirm it.** Reject tests framed purely as "interesting to learn from" with no failing outcome. | *"Remove the two in-article units for this cohort for a week; if engagement doesn't move, any solution resting on the decision-fatigue premise stops."* | *"This would be a super interesting test to run to learn from"*: no outcome ends the solution |
| **LOWER-EFFORT-MVT** | **Ask whether a lower-effort test proves the same point before accepting a build-heavy MVT.** | *"Instead of building the personalised prompt, send a global notification about one preferred-category topic and see if it lifts CTR from the cohort."* | Jumping straight to building the polished solution to test its premise |
| 1 | **Write the priority list of LOFAs/beliefs *before* drafting any test.** Shared LOFAs first, then most-upstream solution-specific LOFA, then gating non-LOFAs, then pre-build. | Priority list at the top, then tests in that order. | Drafting tests in invention order and realising the wrong assumption is tested first. |
| 2 | **Draft in priority order, not invention order.** If a downstream test is easier to picture, that's a signal the upstream one should be tested more cheaply first. | First test = `MVT-<top-LOFA>-1`. | A CTR probe for a mechanism belief when the upstream LOFA is untested. |
| 3 | **Stable test IDs tied to the assumption, not sequential numbers.** | *MVT-F-1*, *MVT-B-1*. Re-ordering doesn't break references. | *1.1, 1.2, 1.3...* Sequential wave names (Wave 1/2/3) are fine; sequential test numbers are not. |
| 4 | **Cheapest test that could kill the assumption** | Existing-data analysis before interviews before fake-door before A/B. A multivariate or A/B test is still an MVT when nothing cheaper settles the assumption, or when the question is which execution wins, not whether the premise holds. | Skipping straight to a build-heavy A/B |
| 5 | **Test must match the assumption type** | Per `pattern-library.md` 1.8 and the solution-specific defaults | Mismatched (e.g. A/B for a desirability assumption) |
| 6 | **Name all three metric tiers** | Leading (proximate signal), lagging (downstream outcome), guardrail (what must not degrade) | A single success threshold |
| 7 | **Explicit decision criteria, per outcome** | *"If CTR and depth rise without a frequency drop, progress; if CTR rises but frequency falls, the value-chain LOFA fired, stop and re-frame."* | *"We'll see what the data shows"* |
| 8 | **Fidelity must match cost of failure** | Cheap test for a cheap solution; high fidelity for irreversible decisions | Low-fidelity test before killing a major product line |
| 9 | **Stage gates only where LOFA tests sit above them.** Each gate evaluates the LOFA test(s) immediately preceding it. A shared-LOFA test gets a single gate: if it fails, every dependent solution is parked together. | Gate after Wave 1 if Wave 1 tests the LOFAs. | Gate after a wave that tests a non-LOFA. |
| 10 | **Separate gating tests from implementation-design work.** Implementation/scope work goes into a "Pre-build analysis" section that runs only after the LOFA gates are green. | Pre-build tests with IDs like *PB-I-1*. | Implementation work mixed into the gating waves. |

### Soft check

- **Cost-of-failure framing.** Before settling on fidelity, ask: *"If we ship this and it's wrong, what does it cost to roll back? What's the brand/customer impact?"*
- **Chain-aware sequencing.** Follow the LOFA dependency chain, not just cost order. No point cheaply testing "does depth convert to retention?" if "is there any depth headroom at all?" is unresolved.
- **Shared-LOFA bonus.** When a single test resolves a LOFA shared across solutions, say so explicitly: it kills or saves several ideas at once and should run upstream of all of them.

---

## Passable-vs-better as a worked pushback rule

The clearest illustration of the belief criteria is one worked critique of a personalised off-platform prompt solution. The LOFAs were strong; three belief problems carried the lesson.

1. **Vague belief (VAGUE-METRIC).** *"Previous tests showed a positive improvement to engagement when notifications were activated."* Critique: *"Was this improvement to frequency or session depth? Be specific."* A belief citing a prior result must name the metric and direction.
2. **Belief disconnected from the mechanism (BELIEF-LINK).** *"Research indicates light-engagement subscribers value their preferred content categories but feel overwhelmed by breaking-news-dominated experiences."* Critique: *"This doesn't clearly explain how it links to the solution of a personalised off-platform prompt."* Route to the value-chain gate.
3. **Unisolated problem (PROBLEM-ISOLATES).** If low prompt CTR is actually a sign-up or opt-in problem, *"the first test isn't to personalise the prompts, it's to test messaging and new sign-up surfaces. The problem hypothesis, defined the step before, would have isolated this CTR problem specifically."* A sharp problem hypothesis upstream decides whether the first solution test is even the right one.

The closing point is the **LOWER-EFFORT-MVT** rule. Once the beliefs are sound, the only open question is whether the personalised prompt is the right MVT given the impact/effort tradeoff. A lower-effort test that proves the same point: send a global notification about one preferred-category topic and see whether it lifts CTR from the cohort. Same learning, far less build.

---

## Escape hatches

When the PM wants to override the pushback:

- **"I've already done this."** Skill asks: *"Can you point me to the doc or note where this was captured?"* If yes, accept and log. If no, gently push back: *"Worth capturing now so future you doesn't have to redo it."*
- **"I'm under time pressure."** Skill accepts but flags: *"Noted, proceeding. Flagging that we skipped [X] which usually catches [Y class of failure]. Worth coming back to if time allows."*
- **"Trust me on this one."** Skill accepts the first time, but logs explicitly. If the same PM overrides repeatedly across sessions, the skill could (in future) surface a pattern.
- **"This doesn't apply to my situation."** Skill asks: *"What's different about your situation? I might be able to adapt the pattern."* This is genuine, patterns aren't universal.

## Override logging format

In the running doc, every override is logged as:

```
Phase X, [date/time]:
  Skill flagged: [criterion]
  PM override: [their reason]
  Risk accepted: [the failure mode this exposes the work to]
```

This makes the override visible if the work fails later. Not to blame the PM, but to inform future iteration of these rules.

---

## Pushback that doesn't apply (overrides automatic)

There are some contexts where the standard reject criteria don't fire:

- **Optimisation mode (not growth experiments).** If the PM is doing pure optimisation (per `pattern-library.md` 1.12), the full decomposition isn't needed. Skill detects this in Phase 0 and routes to the fast path (6a + 7).
- **Returning to existing work.** If the PM is iterating on a previously-mapped tree, earlier phases can be loaded from the running doc and only the new branch needs full processing.
- **Time-boxed exploratory sessions.** If the PM explicitly says "I want to brainstorm quickly, not validate," the skill should still produce the artefacts but mark all beliefs and LOFAs "unvalidated, exploration only" and skip the confidence-rating phase.

---

## Open questions for the next pass

- How aggressive should the skill be when the PM repeatedly overrides the same criterion?
- Should the skill have memory of prior overrides across sessions for the same PM?
- Are there domain-specific reject criteria for monetisation solutions that should be added?
- How to handle the case where multiple PMs collaborate on the same tree (shared overrides, conflicting inputs)?
