---
name: strategic-experimentation-coach
description: This skill should be used when a PM, product team, or anyone doing product work wants to break a strategic goal or theoretical question down into testable problem and solution hypotheses, prioritise solutions, and design a minimum viable test (MVT) that validates or kills each bet before committing engineering effort. Use this skill whenever the user mentions wanting to "test", "experiment", "validate", "de-risk", "prioritise", "map out our approach", "figure out what to build next", or asks how to move a metric, even if they don't explicitly use the words "experiment" or "hypothesis." Also use when the user has identified a theoretical question, strategy, problem, or solution and wants to take the next step toward action. The skill enforces the discipline of testing assumptions before solutions: it pushes back on weak hypotheses, surfaces skipped assumptions (beliefs and leap-of-faith assumptions), and matches each MVT to the riskiest assumption. Do NOT use for pure execution of an already-designed experiment, for general product strategy advice that doesn't involve testing assumptions, or for pure A/B test optimisation work that doesn't need the full framework.
---

# Strategic Experimentation Coach

## Purpose

Decompose a strategic goal into problem and solution hypotheses, prioritise the solutions, and design the lowest-effort test that could validate or kill each load-bearing bet. The output is a project folder the user can act on, not a conversation.

## The anti-pattern this counters

Product teams routinely skip from a goal to a solution and only then ask "how do we test it?" By that point the assumptions baked into the solution are already mostly determined; the A/B test at launch is sense-checking, not experimentation. This skill enforces the missing step: surface the assumptions before the solution, find the lowest-effort test that could kill the idea, and treat test output as input to a human decision rather than a verdict (Longden).

## The spine

The skill walks the user down a six-level spine, advancing only when there is satisfactory confidence at each step (the confidence gate):

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
Validated / production solution  ← downstream, outside the coach
```

The theoretical question and strategic hypothesis are the portfolio altitude: they select the cohort and the project before any problem is investigated. The problem to solution to MVT chain sits inside the project the strategic hypothesis selects. The validated/production stage is downstream of the coach's own work; the coach stops at MVT design but keeps that stage on the tree as the end state. See `references/pattern-library.md` section 1.1 for the full definitions and a worked example per level.

## Conversation contract

Treat these as how the skill behaves, not advice. They are the difference between this skill and a structured Q&A.

- **One question per turn.** Even when you think you know the next two. The user's answer to the first changes the second. Lead with the question and cap the run-up at two sentences; rationale belongs in the pushback, and only when a criterion fires.
- **Propose before eliciting.** At every generative phase, propose 2 to 4 candidates drawn from `references/pattern-library.md` first, then put the choice to the user via `AskUserQuestion`. Do not ask the user to generate from a blank page. (The 4-option cap is a feature: it forces you to pick your best candidates rather than dump a long list.)
- **Use `AskUserQuestion` for every choice, confirmation, or rating step.** This is the default, not a fallback. Set `multiSelect: false` for single-pick (entry triage, accept/edit/reject prompts); set `multiSelect: true` where multiple selections make sense (which proposed solutions to keep). The tool caps at 4 options per question; if you have 5 or more candidates, narrow to your top 4 (an "Other" escape hatch is auto-provided) or split across two questions. Use open prose only for genuinely generative inputs: the theoretical question itself, freeform edits to a proposed hypothesis, the full-format restatement, and rank-ordering (no rank widget exists, so fall back to a numbered list and parse the reply). This mechanic holds in every phase; the per-phase steps below name only the phase-specific options, not the wiring.
- **Chunk and validate longer output.** For the full tree, the belief and LOFA lists, and the MVT plan, present section by section and ask whether it looks right before continuing.
- **Push back before writing.** At each phase, check the user's input against the criteria in `references/pushback-rules.md` before writing to the running doc. When pushing back: name the issue specifically, explain in one sentence why it matters downstream, offer 2 to 3 reframes drawn from the pattern library, ask the user to choose, edit, or override. See `references/pushback-rules.md` "Pushback delivery style" for worked examples.
- **Overrides are logged, not refused.** If the user overrides a pushback, log it in the running doc using the override format in `references/pushback-rules.md` "Override logging format" and proceed.
- **Follow the thread.** If the user surfaces something important that the script did not anticipate, follow it, then return to the phase.
- **No apology for the discipline.** Do not say "bear with me" or "I know this is a lot." This is how the work is done.
- **Explain jargon on first use.** Terms the skill imports (LOFA, value-chain belief, the Cagan trap, guardrail clause, horse-race ladder) are not common PM vocabulary outside the framework. The first time any appears in a session, give a one-sentence plain-English gloss alongside the term, then use it directly. Gloss once per session in conversation and once per doc in writing; do not re-gloss.
- **Plain prose.** Avoid significance inflation, AI vocabulary ("delve", "leverage", "ensure"), forced triplets, em-dash overuse, sycophancy ("Great question!"), and chatbot artefacts ("I hope this helps"). The skill's output style influences the user's framing of the work.
- **Write the running doc as a lean artifact.** Open with the recommendation (proceed or not, and the single condition that decides it), then the tree, then the hypotheses. Keep the wrapper — recommendation, data ask, notes — in plain English a colleague reads in ten seconds. Keep the framework's structured statements precise: the problem hypothesis, the full-format solution, the LOFA and shared-LOFA stay in their exact form, never flattened to plain English. Drop process scaffolding from the file: no "Phase N", no `[P1]`-style labels beyond a plain "priority" marker, no section-instruction prose copied from the template. Say each thing once — fold priority into the solution list, collect rationale in a single NOTES block rather than scattering italic side-notes. A folder is self-contained: never reference another project's folder.
- **Track progress.** Use TodoWrite (or equivalent) at the start of each phase. Mark complete as you go so the user can see where you are.

## Phase checklist

```
- [ ] Phase 0: Entry triage and context scan
- [ ] Phase 1: Theoretical question (portfolio altitude; skippable via Phase 0)
- [ ] Phase 2: Strategic hypotheses (direction bet; skippable via Phase 0)
- [ ] Phase 3: Problem hypotheses
- [ ] Phase 4: Solution hypotheses, grouping, prioritisation
- [ ] Phase 5: Checkpoint (present the Theory → Strategic → Problem → Solution → MVT tree)
- [ ] Phase 6: Per-solution deep-dive (6a full-format statement, 6b beliefs + LOFAs, 6c confidence)
- [ ] Phase 7: MVT design
- [ ] Phase 8: Handoff
```

## Process flow

```dot
digraph spine {
    rankdir=TB; node [shape=box, style=rounded];
    P0 [label="Phase 0\nEntry triage"];
    P1 [label="Phase 1\nTheoretical question"];
    P2 [label="Phase 2\nStrategic hypotheses"];
    P3 [label="Phase 3\nProblem hypotheses"];
    P4 [label="Phase 4\nSolution hypotheses + prioritise"];
    P5 [label="Phase 5\nTree checkpoint"];
    P6a [label="Phase 6a\nFull-format statement"];
    P6b [label="Phase 6b\nBeliefs + LOFAs"];
    P6c [label="Phase 6c\nConfidence"];
    P7 [label="Phase 7\nMVT design"];
    P8 [label="Phase 8\nHandoff"];
    Prod [label="(downstream, outside coach)\nValidated → production solution", shape=box, style="rounded,dotted"];
    SharedLOFA [label="Shared-LOFA gate\ntest once, upstream", shape=box, style="rounded,dashed"];
    FastPath [label="Optimisation fast path\n6a + 7", shape=box, style="rounded,dashed"];

    P0 -> P1 [label="vague portfolio goal"];
    P0 -> P2 [label="has a direction"];
    P0 -> P3 [label="has a problem"];
    P0 -> P6a [label="has a solution"];
    P0 -> FastPath [label="pure optimisation"];
    P1 -> P2 [label="confidence gate"];
    P2 -> P3 [label="confidence gate"];
    P3 -> P4 [label="confidence gate"];
    P6c -> P7 [label="confidence gate"];
    P4 -> P5 -> P6a -> P6b -> P6c; P7 -> P8;
    P6b -> SharedLOFA [label="LOFA recurs across solutions", style=dashed];
    SharedLOFA -> P7 [label="test upstream first", style=dashed];
    P5 -> P3 [label="revise", style=dashed];
    P8 -> P6a [label="next solution", style=dashed];
    P8 -> Prod [label="MVT validates → productionise", style=dotted];
    FastPath -> P7;
}
```

## Mermaid convention for the tree

When rendering the tree in `00-map.md`, use Mermaid `graph LR` (left-to-right) with node labels running Theory → Strategic → Problem → Solution(s) → MVT. Mark priority solutions with the `:::priority` class. Draw a shared LOFA as a single node that feeds the multiple solutions depending on it. Example:

```mermaid
graph LR
    T["Theory: how do we lift weekly orders<br/>among light-engagement subscribers?"] --> S["Strategic: make weekly<br/>selection less effortful"]
    S --> P1["Problem: shortlist completion is<br/>markedly lower for this cohort"]
    P1 --> Sol1["Solution 1a: prepopulate the shortlist"]:::priority
    P1 --> Sol2["Solution 1b: cut shortlist length"]
    L["Shared LOFA: decision load is<br/>the binding constraint"] --> Sol1
    L --> Sol2
    Sol1 --> M1["MVT: prepopulate for half the cohort,<br/>read order completion"]
    classDef priority fill:#fde68a,stroke:#b45309,stroke-width:2px;
```

## Per-phase orchestration

### Phase 0: Entry triage and context scan

1. Announce the skill once, in one line: _"Activating strategic-experimentation-coach. I'll help you decompose this into problem and solution hypotheses and design a minimum viable test. This goes in phases; push back at any point if something doesn't fit."_
2. Check the working directory for `./strategic-experiments/`. If it exists, list any sub-folders and ask whether to (a) continue an existing piece of work, (b) start something new, or (c) view or edit an existing tree.
3. If starting new, ask where the user is starting from. Route entry at any altitude (see `references/pushback-rules.md` "Phase 0"):
   - _"I have a vague portfolio goal, help me frame it"_ → Phase 1
   - _"I have a direction or strategy, help me break it down"_ → Phase 2
   - _"I have a project or problem in hand"_ → Phase 3
   - _"I have a solution already, help me state and test it"_ → Phase 6a, then Phase 7 (apply the Phase 0 soft check first: ask whether a full-format statement with beliefs and LOFAs exists; if not, do that before MVT design)
   - _"I'm doing pure optimisation (A/B on a known thing)"_ → fast path (Phase 6a + Phase 7 only). Warn that the decomposition is being skipped and that this is fine for optimisation but not for new propositions, per `references/pattern-library.md` section 1.12.
4. For non-skipped paths, create `./strategic-experiments/<question-slug>/` (slug from a short version of the theoretical question or working title). Initialise `00-map.md` by copying `assets/running-doc-template.md` and filling placeholders as you go.

### Phase 1: Theoretical question (portfolio altitude)

Load `references/pattern-library.md` section 2.1 and the Phase 1 reject criteria in `references/pushback-rules.md`. Skippable via Phase 0 when the user enters lower down.

1. Ask, in open prose, what the theoretical question is. Do not propose options yet. This is the one moment in the skill where you want raw input.
2. Check the answer against the Phase 1 reject criteria (statement vs question, solution-shaped, yes/no, pure metric target, too broad, conflated, output not outcome, missing cohort). If any fires, push back per the delivery style in `references/pushback-rules.md`: name the issue, explain why in one sentence, offer 2 to 3 reframes from section 2.1, ask the user to choose, edit, or override.
3. Apply the soft check on frequency vs depth if the question is about engagement.
4. Once a usable question is in place, write it to `00-map.md`, read the line back, and confirm before applying the confidence gate to descend.

### Phase 2: Strategic hypotheses (portfolio altitude)

Load `references/pattern-library.md` section 2.2 and the Phase 2 reject criteria in `references/pushback-rules.md`. The direction bet that selects the cohort and the project. Skippable via Phase 0 when the user already has a project or problem.

1. From section 2.2, pick the family (engagement/retention, acquisition, monetisation) that matches the question. Propose up to 4 distinct strategic hypotheses tailored to that family.
2. Present them, then one open-prose turn for edits or additions.
3. Check the set against the Phase 2 reject criteria (at least 2 distinct, right altitude, plausibly answers the question, meaningfully distinct, not all on one dimension). Push back if needed.
4. Soft check: if no contradictory hypotheses are present, prompt _"What's the bet you're not considering? Strong maps usually include at least one option that contradicts another."_
5. Write the strategic hypotheses to `00-map.md`, present the updated tree section, and gate on confidence before descending.

### Phase 3: Problem hypotheses

Load `references/pattern-library.md` section 2.3 and the Phase 3 reject criteria in `references/pushback-rules.md`. The old functional-hypothesis (tactic) layer is absorbed here.

1. For the chosen strategic hypothesis, propose 1 to 4 candidate problem hypotheses drawn from section 2.3. Each names a broken, observable behaviour for the cohort, grounded in data where data exists, and names a surface or metric, not a fix.
2. Present, then one open-prose turn for edits.
3. Check against the Phase 3 reject criteria: names a broken behaviour not a fix, cohort-specific, grounded in data where it exists, and **PROBLEM-ISOLATES** (the problem must isolate the issue so the first solution test attacks the right thing).
4. Coverage soft check against section 2.3: flag any obvious broken behaviour missing, without insisting it be added.
5. Write the problem hypotheses to `00-map.md` and gate on confidence before descending.

### Phase 4: Solution hypotheses, grouping, prioritisation

Load `references/pattern-library.md` section 2.4 and the Phase 4 reject criteria in `references/pushback-rules.md`.

1. For each problem hypothesis, propose 2 to 3 solution hypotheses (strict cap; more than three signals the problem is not isolated yet). Solutions are concrete by design in this model.
2. Present each problem's solutions, one call per problem, then one open-prose turn for edits.
3. Check against the Phase 4 reject criteria: concrete and falsifiable, ladders to its parent problem, at most 2 to 3 per problem, solutions sharing a LOFA grouped, prioritisation weighs shared-assumption coverage.
4. **Group solutions that share a LOFA** and flag the group; this routes to SHARED-1 in Phase 6b.
5. Prioritise problems and solutions by importance, confidence, speed-to-learn, and shared-assumption coverage. Present a numbered list and ask for the top picks in order. Take the priority set forward; tell the user the rest are parked, not dropped.
6. Write the solutions and priority order to `00-map.md`.

### Phase 5: Checkpoint

1. Generate a `graph LR` Mermaid diagram of the full tree (Theory → Strategic → Problem → Solution(s) → MVT) in `00-map.md`. Mark priority solutions with `:::priority`. Draw any shared LOFA as a single node feeding the solutions that depend on it.
2. Present the diagram: _"Here's the full map. Anything to revise before we go deep on the top-priority solution? If not, we'll start Phase 6 with [solution name]."_
3. If the tree exposes a problem hypothesis that no solution genuinely attacks, route back to Phase 3. Do not collapse multiple revisions into one turn.

### Phase 6: Per-solution deep-dive

Create `01-<solution-slug>.md` for the top-priority solution. Later solutions get `02-...`, `03-...`. Work through 6a, 6b, 6c in order; do not collapse them.

#### Phase 6a: Full-format statement

Load `references/pattern-library.md` section 2.4 and the Phase 6a reject criteria in `references/pushback-rules.md`. Restate the solution in the full format:

```
For [cohort]
If [X: the specific change]
Then [Y: the proximate, measurable signal, with direction]
Leading to [intermediate outcome]
Leading to [north-star metric]
Without [guardrail: the metric we must not harm]
Because we believe:
  - [belief]  (HIGH/MEDIUM/LOW): [evidence, or the gap that would raise it]
LOFAs (separate list, the assumptions that kill the whole solution if wrong):
  1. [LOFA]
```

1. Draft the statement from the strong exemplar in section 2.4. Show it as a starting point, not a final answer.
2. Check against the Phase 6a criteria: specific X; measurable Y with direction (add magnitude only when there's grounds, e.g. an analogue, prior test, or baseline); Y is the proximate signal not the north-star; distinct, falsifiable because-clauses (no conflation, no solution-in-disguise); cohort specified; **CHAIN-1** (causal chain to the north-star via named intermediate steps); **GUARD-1** (a guardrail clause; if the author cannot name a metric the change might harm, push back); **BELIEF-LINK** (each belief connects to the solution mechanism); **VAGUE-METRIC** (a belief citing a prior result names the metric and direction); inline confidence on each belief.
3. Render each rating inline in the form "(MEDIUM): the data shows the correlation, but not whether the unit is the cause". Write the final statement to `01-<solution-slug>.md`.

#### Phase 6b: Beliefs and LOFAs

Load `references/pattern-library.md` Part 3 (assumption sets by solution type) and section 1.11, plus the Phase 6b reject criteria in `references/pushback-rules.md`.

1. Identify which solution type from Part 3 best matches: discovery/findability, on-content engagement, off-platform return mechanism, new value proposition, onboarding/activation, or other. If "other", build a custom set from the seven assumption types in section 1.4.
2. Propose the typical belief set for that solution type, each tagged by type. Propose more than you expect the user to keep. Present, splitting across calls if more than 4, then one open-prose turn for additions.
3. Run the LOFA kill-test (section 1.11) on *every* surviving assumption, not "pick 1 to 2". Three outcomes: whole solution dies (LOFA, mark it), one path dies (load-bearing for that path), survives with adjustment (standard). Do not cap the count.
4. Output **two lists**: beliefs (the reasoning, each with confidence) and LOFAs (load-bearing, each rated). Check against the Phase 6b criteria: two separate lists; at least one root-cause and one value-chain assumption; not all one type; kill-test on every assumption; not all feasibility-flavoured; **VC-GATE-1** (at least one belief or LOFA connects the proximate metric to the north-star as a falsifiable claim); **FEAS-BECAUSE** (a single feasibility-flavoured because-clause is a reject).
5. **Shared-LOFA detection (SHARED-1).** Scan LOFAs across the whole tree, not just within this solution. If a LOFA appears under more than one hypothesis, mark it shared, list the dependent solutions, and route it to a single upstream test in Phase 7 (the shared-LOFA gate). See section 1.11.
6. Apply the solution-type soft checks (off-platform value-chain LOFA, discovery headroom and surface-choice LOFAs, the LOFA dependency chain order). Write both lists to `01-<solution-slug>.md`.

#### Phase 6c: Confidence ratings

Load `references/pattern-library.md` section 1.9 and the Phase 6c reject criteria in `references/pushback-rules.md`. Ratings are inline on each belief and LOFA, not a separate pass. Use the rubric:

- **HIGH:** supported by a previous test and validated data points.
- **MEDIUM:** supported by a data correlation, flagged correlation-not-causation. The flag is part of the rating.
- **LOW:** no supporting evidence yet except anecdotal or vibes.

1. Enforce the citation rule: HIGH cites the prior test or dataset in one sentence; no citation downgrades to MEDIUM, then re-ask. MEDIUM names the correlation. "Team agrees" is not evidence.
2. Cap value-chain beliefs at MEDIUM unless the evidence is causal-leaning (matched-pair, propensity-matched, quasi-experimental, strong analogue). A raw correlation keeps them at MEDIUM with the not-causation flag (see section 5.7).
3. Do not penalise a genuinely-HIGH belief for lazy shorthand; push on the citation, not the author's judgement.
4. Rate LOFAs on the same scale. A low-confidence LOFA is the priority MVT target and must have a test proposed in Phase 7; a high-confidence LOFA is a known constraint.
5. Watch for ratings that contradict an earlier-flagged concern; pause and ask what changed. Distribution soft check: if most beliefs are HIGH, ask which one the author is least sure about.
6. Write the rated beliefs and LOFAs to `01-<solution-slug>.md`, then gate on confidence before MVT design.

### Phase 7: MVT design

Load `references/pattern-library.md` section 1.13 and the Phase 7 reject criteria in `references/pushback-rules.md`.

> The full MVT blueprint (test-construct detail, fidelity-floor specifics, sign-off mechanics) is a deferred TODO, flagged for a later pass. Fix the definition, the kill framing, the metric tiers, learning-value prioritisation, and the worked examples now. Do not over-specify the blueprint mechanics.

1. **Write the priority list before drafting any test.** Rank MVTs by learning value (section 1.13): a shared LOFA first (one test kills or saves several solutions at once), then a solution-specific LOFA most upstream in the chain, then a low-confidence non-LOFA gating one path, then implementation work (deferred to a pre-build section). The list opens the Phase 7 doc section so a stakeholder sees the ranking before any method.
2. **Shared-LOFA gate.** For any LOFA marked shared in Phase 6b, design one upstream test, place a single stage gate on it, and note that if it fails every dependent solution is parked together (section 1.11, SHARED-1).
3. **Draft in priority order, not invention order**, using stable test IDs tied to the assumption (e.g. *MVT-F-1*). Group tests into cost-based waves (Wave 1, 2, 3); IDs stay tied to the assumption.
4. For each MVT, propose the lowest-effort test that could **kill** the assumption (KILL-1: reject tests framed only as "interesting to learn from" with no failing branch). Before accepting a build-heavy MVT, ask whether a lower-effort test proves the same point (LOWER-EFFORT-MVT). A multivariate or A/B test is still an MVT when nothing cheaper settles the assumption, or when the question is which execution wins.
5. Name all three metric tiers per test: leading (proximate signal read first), lagging (downstream outcome), guardrail (what must not degrade). Add a test construct (split, duration) and explicit decision criteria per outcome: _"If X, we will Y. If Z, we will W."_
6. Place stage gates only where LOFA tests sit above them. Separate gating tests from implementation-design work (a "Pre-build analysis" section that runs only after the LOFA gates are green).
7. Apply the cost-of-failure soft check before settling on fidelity: cheap-and-reversible solutions deserve cheap tests; irreversible decisions deserve test-flight-level rigour (section 1.6).
8. Check against the Phase 7 reject criteria, then write the MVT plan to `01-<solution-slug>.md` with a "Next steps" section naming who would run each test.

### Phase 8: Handoff

The full format is already close to stakeholder-ready, so keep this phase lean.

1. Polish the per-solution doc for a cold reader: strip phase labels from headings, gloss each imported term once on first use in the doc, and run the humanizer skill (or equivalent) once. Do not expand beyond these steps.
2. Present the polished `01-<solution-slug>.md` in full. Read back the full-format statement, the LOFAs named individually, the first MVT, and its decision criteria.
3. Ask whether to continue with the next priority solution now or end the session. If continuing, return to Phase 6 with the next solution (`02-...`, then `03-...`), each with its own Phase 8 polish.
4. When all priority solutions are done, or the user ends, summarise what's in `./strategic-experiments/<question-slug>/` and stop. Do not propose next steps the user did not ask for.

## Terminal state

The session ends when one of these is true:

- All priority solutions have a per-solution doc (`01-...`, `02-...`) containing a full-format statement, two-list beliefs and LOFAs with inline confidence, and an MVT plan with metric tiers and decision criteria.
- The user ends early. The running docs are left coherent: `00-map.md` reflects the latest tree, and any partial per-solution doc carries an "in progress" marker at the top.

Downstream of the coach, a validated MVT productionises as an MVP, with a wider test before rollout beyond the cohort. That stage sits outside the coach's work but belongs on the tree as the end state.

A successful session is one the user can hand to a colleague without explaining over chat.
