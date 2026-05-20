# Strategic Experimentation Skill: Pushback Rules

**Version:** 0.2
**Status:** Draft, iterate as the skill is used
**Purpose:** Codifies what the skill rejects, why, and how, at each phase of the conversation. The skill's pushback is its core value. Without it, the skill is just a structured Q&A; with it, the skill enforces the discipline that PMs typically skip.

---

## How to use this document

This is a living rulebook. As the skill is used:

- If a PM-team conversation surfaces a category of weak input not covered here, add it.
- If a reject criterion is firing too often on legitimate inputs, soften it.
- If a reject criterion is *not* firing when it should, sharpen it.

Each phase below lists: the criteria, what the skill says when triggered, and worked examples of good vs. bad inputs.

---

## Changelog

- **v0.2**, Loosened Phase 5a rules on magnitude and because-clause count. Added a sixth core principle on precision. Removed em dashes throughout.
- **v0.1 (initial)**, drafted from synthesis of Cagan, Torres, Bland, Gilad, and Longden/Speero frameworks.

---

## Core principles

1. **Pushback is in service of the PM's success, not skill stubbornness.** Every rejection must explain why and offer reframes. Never reject without giving the PM a way forward.
2. **Aggressive on the discipline, generous on the assumptions about the PM.** Assume the PM is smart, busy, and would do this right if they had the time. Don't lecture.
3. **The skill is not the decider.** PMs can override any pushback with a stated reason. Log the override; don't refuse to proceed.
4. **Sanity checks beat exhaustive checks.** It's better to surface one critical issue clearly than five marginal issues exhaustively.
5. **Show, don't tell.** When rejecting, propose 2–3 specific reframes rather than abstract principles.
6. **Precision where it earns its keep.** Insist on falsifiability and distinctness. Don't insist on numeric magnitudes the team has no basis for, or a fixed count of because-clauses. Made-up precision is worse than honest 'we don't know yet'.

## Pushback delivery style

When the skill detects a reject criterion firing, it should:

1. **Name the issue specifically.** Not "this isn't quite right" but "this names a solution rather than a question."
2. **Explain why it matters in one sentence.** Why does this distinction affect the work downstream?
3. **Offer 2–3 reframes**, drawn from `pattern-library.md` where possible.
4. **Ask the PM to choose, edit, or override.**

**Example of good pushback delivery:**

> *"'Should we build a Discover page?' names a solution rather than a question, which constrains us to that one direction before we've explored whether discovery is actually the right lever. A few reframes:*
> - *'How can we make content easier for cool subscribers to discover?'*
> - *'Why do cool subscribers fail to find content they'd enjoy?'*
> - *'What's stopping cool subscribers from engaging more deeply?'*
> *Want to go with one of these, edit, or stick with the original?"*

**Example of bad pushback delivery:**

> *"Your theoretical question doesn't conform to the patterns in this framework. Please revise it to be outcome-focused and to admit multiple solution directions."*

(Why bad: abstract, doesn't say what's wrong, doesn't give the PM anything to work with.)

---

## Phase 0, Entry triage

No real pushback here, just routing. The skill asks where the PM is starting (vague problem / have a question or strategy / have tactics, want experiments) and routes accordingly.

**One soft check:** if the PM says "I have tactics, just help me design experiments," the skill should ask: *"Quick check: do you have a clear hypothesis statement for each tactic, with the underlying assumptions identified? If not, we should do that first; experiment design without it tends to test the wrong things."* This is the only escape hatch with a guard rail on it.

---

## Phase 1, Theoretical question

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **Must be a question, not a statement** | *"How can we increase engagement among cool subscribers?"* | *"We need to increase engagement among cool subscribers."* |
| 2 | **Must be outcome-focused, not solution-focused** | *"How can we make content easier for cool subscribers to discover?"* | *"Should we build a Discover page?"* |
| 3 | **Must not be yes/no** | *"What would happen if we changed our free tier?"* | *"Should we cut the free tier?"* |
| 4 | **Must not be a pure metric target** (it can reference a metric, but not be one) | *"How can we grow our active user base among [cohort]?"* | *"How do we get to 1M DAU?"* |
| 5 | **Must be narrow enough to be tractable** | *"How do we grow [cohort] over [timeframe]?"* | *"How do we grow?"* |
| 6 | **Must not conflate multiple questions** | Pick one of two | *"How do we acquire younger users and retain them better?"* |
| 7 | **Must be about outcomes, not outputs** | *"How do we increase engagement?"* | *"How do we ship more features?"* |
| 8 | **Should specify a cohort or segment where relevant** | *"...among cool subscribers"* | *"...among users"* (when the team isn't actually trying to move everyone) |

### Soft check (not a reject, but flag)

- **Frequency vs depth conflation in engagement questions.** If the PM's question covers both ("how do we increase engagement"), the skill should ask: *do you mean frequency, depth, or both? They have different hypotheses and metrics, worth splitting unless you have reason to keep them together.*

---

## Phase 2, Strategic hypotheses

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

## Phase 3, Functional hypotheses (tactics)

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **Must be tactics, not solutions** | *"Make it easier for users to find content they want"* | *"Build a Discover page"* |
| 2 | **Must ladder up to a parent strategic hypothesis** | The tactic is recognisably a way to pursue the parent direction | The tactic could appear under any strategic hypothesis |
| 3 | **Must be at the right altitude**, can generate 3+ specific solutions | A tactic generates Discover page, homepage personalisation, recommendations, etc. | A tactic that has only one obvious implementation |
| 4 | **Must be specific enough to test** | Names a lever and a target segment | Vague like *"improve UX"* |
| 5 | **Should not be a list of features in disguise** | A small set of tactics, each generative | A long list where each item is one feature |

### Soft check

- **Coverage check.** Across the tactics in this branch, are the obvious levers covered? The skill should compare the PM's tactic list to the patterns in `pattern-library.md` Part 2.3 and flag if a common lever is missing, without insisting it be added.

---

## Phase 5a, Hypothesis restatement (if-then-because)

After tactic prioritisation, each priority tactic is restated as *"If X, then Y, because A, B, C."*

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **Must follow if-then-because structure** | Has all three clauses | Missing one or more |
| 2 | **X must be specific** | *"Add a personalised Discover surface to the homepage for cool subscribers"* | *"Improve discovery"* |
| 3 | **Y must be measurable with direction. Add magnitude only when there's grounds for one** | *"'...weekly order completion will rise 10–15% in this cohort over 6 weeks' (when anchored in baseline data); or '...weekly order completion will rise materially in this cohort over 6 weeks; magnitude TBD pending baseline'"* | *"'...engagement will go up' (no direction); or '...will rise 22% over 8 weeks' with no analogue or baseline to anchor that number"* |
| 4 | **Y must be a proximate metric** that could plausibly move on the experiment's timescale | Scroll depth, articles per session, return rate over 4 weeks | LTV, annual retention (too downstream for a single experiment) |
| 5 | **Must have 2 or more distinct because-clauses (usually 2–5)** | Three clauses, each separately testable | One conflated clause covering multiple assumptions; or a forced fifth clause padded in to hit a count |
| 6 | **Because-clauses must be falsifiable** | *"...light-engagement subscribers will engage with the prepopulated shortlist at rates close to fully-engaged subscribers"* | *"...because it would be better"* |
| 7 | **Because-clauses must not be solutions in disguise** | *"...because discovery friction is the binding constraint"* | *"...because users want a Discover page"* |
| 8 | **Should specify the cohort** | *"...among cool subscribers"* | *"...among users"* |

### Soft check

- **Made-up precision.** If the magnitude has no anchoring evidence (analogue, prior test, baseline), prefer 'TBD pending baseline' over an invented number. Fabricated thresholds anchor decisions later and read as false confidence.

---

## Phase 5b, Assumption list

For each priority tactic, the PM lists assumptions. The skill helps surface them and propose more from `pattern-library.md` Part 3.

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **Must have at least 5 assumptions** | Most tactics have 5–10 | Fewer than 5 (almost always means hidden assumptions) |
| 2 | **Must include at least one root-cause assumption** | *"The drop-off is because of X, not Y or Z"* | Only problem/desirability/mechanism types |
| 3 | **Must include at least one value-chain assumption** | *"The proximate metric → business metric"* | All assumptions are about the immediate intervention |
| 4 | **Must not all be of one type** | Mix of problem, root-cause, desirability, mechanism, magnitude, value-chain | All desirability, or all mechanism |
| 5 | **Must label each assumption by type** | Each one tagged | Untyped list |
| 6 | **Must identify LOFAs** | 1–2 marked as "load-bearing" | None marked |
| 7 | **Must be actual assumptions, not statements of fact** | *"We believe..."* or *"It's true that..."* with uncertainty | Things the team already knows from data; should be cited as evidence, not listed as assumptions |
| 8 | **Must not be all feasibility-flavoured** (Cagan trap) | Mix of risk types | All about whether engineering can build it |

### Soft check

- **Cross-reference the tactic type.** If the tactic is "off-platform touchpoint," does the assumption list include the value-chain assumption that the touchpoint causally drives return visits (not just correlates)? If not, surface it explicitly. This is the most commonly skipped assumption in this category.

---

## Phase 5c, Confidence ratings

For each assumption, the PM rates evidence as High / Medium / Low / None.

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **High-confidence assumptions must cite evidence** | *"High: we have funnel data from Q3 showing X, plus user research from Y"* | *"High: we just know"* |
| 2 | **Not all High** | Realistic mix; usually 1–3 High at most for a new tactic | Everything rated High (almost certainly overconfidence) |
| 3 | **"Team agrees" is not evidence** | Cite data, research, or analogous case | *"High: the team is aligned on this"* |
| 4 | **Confidence rating should reflect causal evidence for value-chain assumptions** | High only if matched-pair, quasi-experimental, or strong analogous evidence | High based on raw correlation |
| 5 | **LOFAs with low confidence must have an experiment proposed** | Skill moves to experiment design for each | Marked low-confidence but no test planned |

### Soft check

- **Distribution check.** If the PM rates 80%+ of assumptions as High, the skill should ask: *"That's a lot of high-confidence assumptions for new work. A few of these might be worth re-examining. Which would you say is the one you're least sure about?"* This is a gentle nudge, not a hard reject.

---

## Phase 6, Experiment design

For each low-confidence high-importance assumption, the skill proposes the lightest experiment that could falsify it.

### Reject criteria

| # | Criterion | What good looks like | What bad looks like |
|---|---|---|---|
| 1 | **Must propose the cheapest test that could falsify the assumption** | Existing data analysis before user interviews before fake-door before A/B | Skipping straight to A/B |
| 2 | **Test must match the assumption type** | Per the matrix in `pattern-library.md` 1.8 | Mismatched (e.g., A/B test for a desirability assumption) |
| 3 | **Must have explicit decision criteria** | *"If X happens, we Y; if Z happens, we W"* | *"We'll see what the data shows"* |
| 4 | **Experiment fidelity must match cost of failure** | Cheap test for cheap tactic; high-fidelity for irreversible decisions | Low-fidelity test before killing a major product line |
| 5 | **Must specify success threshold** | A numeric threshold or direction with magnitude | *"If it goes up"* |
| 6 | **Should sequence experiments** | Cheapest assumption tests first, gating later expensive ones | Parallel build-everything approach |

### Soft check

- **Cost-of-failure framing.** Before settling on experiment fidelity, the skill should ask: *"If we ship this and it's wrong, what does it cost to roll back? What's the brand/customer impact?"* This calibrates the fidelity level (per Longden's principle).

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

- **Optimisation mode (not growth experiments).** If the PM is doing pure optimisation (per `pattern-library.md` 1.12), the full theoretical-question decomposition isn't needed. Skill should detect this in Phase 0 and skip Phases 1–3, going straight to hypothesis restatement and experiment design.
- **Returning to existing work.** If the PM is iterating on a previously-mapped tree, earlier phases can be loaded from the running doc and only the new branch needs full processing.
- **Time-boxed exploratory sessions.** If the PM explicitly says "I want to brainstorm quickly, not validate," the skill should still produce the artefacts but with all assumptions marked "unvalidated, exploration only" and skip the confidence-rating phase.

---

## Open questions for v0.2

- How aggressive should the skill be when the PM repeatedly overrides the same criterion?
- Should the skill have memory of prior overrides across sessions for the same PM?
- Are there domain-specific reject criteria for monetisation tactics that should be added?
- How to handle the case where multiple PMs collaborate on the same tree (shared overrides, conflicting inputs)?
