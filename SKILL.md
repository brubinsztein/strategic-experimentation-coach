---
name: strategic-experimentation-coach
description: This skill should be used when a PM, product team, or anyone doing product work wants to break down a strategic goal or theoretical question into testable hypotheses, prioritise tactics, and design lightweight experiments before committing engineering effort. Use this skill whenever the user mentions wanting to "test", "experiment", "validate", "de-risk", "prioritise tactics", "map out our approach", "figure out what to build next", or asks how to move a metric, even if they don't explicitly use the words "experiment" or "hypothesis." Also use when the user has identified a theoretical question, strategy, or set of tactics and wants to take the next step toward action. The skill enforces the discipline of testing assumptions before solutions: it pushes back on weak hypotheses, surfaces skipped assumptions, and matches experiments to risks. Do NOT use for pure execution of an already-designed experiment, for general product strategy advice that doesn't involve testing assumptions, or for pure A/B test optimisation work that doesn't need the full framework.
---

# Strategic Experimentation Coach

## Purpose

Decompose a strategic goal into testable hypotheses, prioritise tactics, and design the cheapest experiment that could falsify each load-bearing assumption. The output is a project folder the user can act on, not a conversation.

## The anti-pattern this counters

Product teams routinely skip from a goal to a solution and only then ask "how do we test it?" By that point the assumptions baked into the solution are already mostly determined; the A/B test at launch is sense-checking, not experimentation. This skill enforces the missing step: surface the assumptions before the solution, find the cheapest test that could kill the idea, and treat experiment output as input to a human decision rather than a verdict (Longden).

## Conversation contract

Treat these as how the skill behaves, not advice. They are the difference between this skill and a structured Q&A.

- **One question per turn.** Even when you think you know the next two. The user's answer to the first changes the second.
- **Propose before eliciting.** At every generative phase, propose 2–4 candidates drawn from `references/pattern-library.md` first, then put the choice to the user via `AskUserQuestion`. Do not ask the user to generate from a blank page. (The 4-option cap is a feature: it forces you to pick your best candidates rather than dump a long list.)
- **Use `AskUserQuestion` for every choice, confirmation, or rating step.** This is the default, not a fallback. Set `multiSelect: false` for single-pick (entry triage, confidence rating per assumption, accept/edit/reject prompts); set `multiSelect: true` where multiple selections make sense (which proposed tactics to keep). The tool has a hard cap of 4 options per question. If you have 5+ candidates to present, either narrow to your top 4 (an "Other" escape hatch is auto-provided) or split across two questions. Use open prose only for genuinely generative inputs: the theoretical question itself, freeform edits to a proposed hypothesis, the if-then-because restatement, and rank-ordering (no rank widget exists, so fall back to a numbered list and parse the reply). Never present a wall of options in prose when a question with options would do.
- **Chunk and validate longer output.** For the full tree, the assumption list, and the experiment plan, present section by section and ask whether it looks right before continuing.
- **Push back before writing.** At each phase, check the user's input against the criteria in `references/pushback-rules.md` before writing to the running doc. When pushing back: name the issue specifically, explain in one sentence why it matters downstream, offer 2–3 reframes drawn from the pattern library, ask the user to choose, edit, or override. See `references/pushback-rules.md` "Pushback delivery style" for worked examples.
- **Overrides are logged, not refused.** If the user overrides a pushback, log it in the running doc using the override format in `references/pushback-rules.md` "Override logging format" and proceed.
- **Follow the thread.** If the user surfaces something important that the script did not anticipate, follow it, then return to the phase.
- **No apology for the discipline.** Do not say "bear with me" or "I know this is a lot." This is how the work is done.
- **Explain jargon on first use.** Terms the skill imports (LOFA, value-chain assumption, magnitude assumption, root-cause assumption, "the Cagan trap", horse-race ladder) aren't common PM vocabulary outside the framework. The first time any of these appears in a session, give a one-sentence plain-English gloss alongside the term. After that, use the term directly. Do not pre-emptively explain every term up front, just gloss as each one comes up.
- **Plain prose.** Avoid significance inflation ("pivotal", "transformative", "seamless"), AI vocabulary ("delve", "leverage", "navigate", "ensure"), forced triplets, em-dash overuse, sycophancy ("Great question!"), and chatbot artefacts ("I hope this helps"). The skill's output style influences the user's framing of the work.
- **Track progress.** Use TodoWrite (or equivalent) at the start of each phase. Mark complete as you go so the user can see where you are.

## Phase checklist

- [ ] Phase 0 — Entry triage and context scan
- [ ] Phase 1 — Theoretical question
- [ ] Phase 2 — Strategic hypotheses
- [ ] Phase 3 — Functional hypotheses (tactics) and prioritisation
- [ ] Phase 4 — Checkpoint: present the Mermaid tree
- [ ] Phase 5 — Per-tactic deep-dive (5a hypothesis restatement, 5b assumption list, 5c confidence ratings)
- [ ] Phase 6 — Experiment design
- [ ] Phase 7 — Handoff

## Process flow

```dot
digraph strategic_experimentation_flow {
    rankdir=TB;
    node [shape=box, style=rounded];

    P0 [label="Phase 0\nEntry triage"];
    P1 [label="Phase 1\nTheoretical question"];
    P2 [label="Phase 2\nStrategic hypotheses"];
    P3 [label="Phase 3\nTactics + prioritise"];
    P4 [label="Phase 4\nMermaid checkpoint"];
    P5a [label="Phase 5a\nIf-then-because"];
    P5b [label="Phase 5b\nAssumption list"];
    P5c [label="Phase 5c\nConfidence + evidence"];
    P6 [label="Phase 6\nExperiment design"];
    P7 [label="Phase 7\nHandoff"];
    FastPath [label="Optimisation fast path\n5a + 6 only", shape=box, style="rounded,dashed"];

    P0 -> P1 [label="vague problem"];
    P0 -> P2 [label="question framed"];
    P0 -> P5a [label="tactics chosen"];
    P0 -> FastPath [label="pure optimisation"];
    P1 -> P2 -> P3 -> P4 -> P5a -> P5b -> P5c -> P6 -> P7;
    P4 -> P1 [label="revise", style=dashed];
    P4 -> P2 [label="revise", style=dashed];
    P4 -> P3 [label="revise", style=dashed];
    P7 -> P5a [label="next tactic", style=dashed];
    FastPath -> P6;
}
```

## Mermaid convention for the tree

When rendering the tree in `00-map.md`, use Mermaid `graph LR` (left-to-right). Mark priority tactics with the `:::priority` class. Example:

```mermaid
graph LR
    Q["How can we increase engagement frequency<br/>among cool subscribers?"] --> A["Improve return mechanisms"]
    Q --> B["Give new reasons to return"]
    A --> A1["Improve push quality"]:::priority
    A --> A2["Improve newsletters"]
    B --> B1["Exclusive content"]
    classDef priority fill:#fde68a,stroke:#b45309,stroke-width:2px;
```

## Per-phase orchestration

### Phase 0 — Entry triage and context scan

1. Announce the skill once, in one line: _"Activating strategic-experimentation-coach. I'll help you decompose this into testable hypotheses and design experiments. This goes in phases — push back at any point if something doesn't fit."_
2. Check the working directory for `./strategic-experiments/`. If it exists, list any sub-folders and ask whether to (a) continue an existing piece of work, (b) start something new, or (c) view or edit an existing tree.
3. If starting new, ask where the user is starting from using `AskUserQuestion` with `multiSelect: false` and these four options:
   - _"I have a vague problem or goal, help me frame it"_ → Phase 1
   - _"I have a theoretical question or strategy, help me break it down"_ → Phase 2
   - _"I have tactics already, help me design experiments"_ → Phase 5 (apply the Phase 0 soft check from `references/pushback-rules.md` "Phase 0" before accepting)
   - _"I'm doing pure optimisation (A/B on a known thing), skip the framework"_ → fast path (Phase 5a + Phase 6 only). Warn the user that the decomposition is being skipped and that this is fine for optimisation but not for new propositions, per `references/pattern-library.md` section 1.12.
4. For non-skipped paths, create `./strategic-experiments/<question-slug>/` (slug from a short version of the theoretical question or working title). Initialise `00-map.md` by copying `assets/running-doc-template.md` and filling in placeholders as you go.

### Phase 1 — Theoretical question

Load `references/pattern-library.md` section 2.1 and the Phase 1 reject criteria in `references/pushback-rules.md`.

1. Ask the user, in open prose, what their theoretical question is. Do not propose options yet. This is the one moment in the skill where you want raw input.
2. Check the answer against the Phase 1 reject criteria (statement vs question, solution-shaped, yes/no, pure metric target, too broad, conflated, output not outcome, missing cohort). If any criterion fires, push back per the delivery style in `references/pushback-rules.md`:
   - Name the issue (e.g. "this names a solution rather than a question").
   - Explain why in one sentence.
   - Offer 2–3 reframes drawn from section 2.1 anti-pattern table.
   - Ask the user to choose, edit, or override.

   Example. User says "Should we build a Discover page?" Push back: "That names a solution rather than a question, which locks us into one direction before we've checked discovery is the right lever. A few reframes: 'How can we make content easier to discover for cool subscribers?' / 'Why do cool subscribers fail to find content they'd enjoy?' / 'What's stopping cool subscribers from engaging more deeply?' Want one of these, edit, or stick with the original?"
3. Apply the soft check on frequency vs depth if the question is about engagement.
4. Once a usable question is in place, write it to `00-map.md` and read the line back so the user can confirm.

### Phase 2 — Strategic hypotheses

Load `references/pattern-library.md` section 2.2 and Phase 2 reject criteria in `references/pushback-rules.md`.

1. From section 2.2, pick the family (engagement/retention, acquisition, monetisation) that matches the user's question. Propose up to 4 distinct strategic hypotheses tailored to that family (cap at 4 to fit the `AskUserQuestion` options limit; if you genuinely have 5, drop the weakest and note it).
2. Present them via `AskUserQuestion` with `multiSelect: true` so the user can pick which to keep, then follow up with one open-prose turn for edits or additions. Don't ask "accept, edit, add, or reject?" as freeform.
3. Check the resulting set against the Phase 2 reject criteria (at least 2 distinct, right altitude, plausibly answers the question, meaningfully distinct, not all on one dimension). Push back if needed.
4. Apply the soft check: are any contradictory hypotheses present? If not, prompt: _"What's the bet you're not considering? Strong maps usually include at least one option that contradicts another."_
5. Write the strategic hypotheses to `00-map.md`. Present the updated tree section back.

### Phase 3 — Functional hypotheses (tactics) and prioritisation

Load `references/pattern-library.md` section 2.3 and Phase 3 reject criteria in `references/pushback-rules.md`.

1. For each strategic hypothesis, propose 2–4 candidate tactics drawn from the patterns. Present each parent hypothesis's tactics via `AskUserQuestion` (`multiSelect: true`, max 4 options) so the user picks which to keep. Run one call per parent hypothesis rather than packing all tactics into one question.
2. Follow up with one open-prose turn for any edits or additions the user wants to make.
3. Check against Phase 3 reject criteria: tactics not solutions, ladders to parent, right altitude (can generate 3+ specific solutions), specific enough to test, not a feature list in disguise.

   Example. If the user replies "Build a Discover page" under "improve existing value", push back: "That's a solution, not a tactic. The parent direction asks how we improve existing value; a tactic at the right altitude would be 'reduce friction of finding the content users want' or 'make it easier to discover content users might enjoy but haven't found' — Discover page is one solution under either of those. Want to lift to the lever level?"
4. Apply the coverage soft check against section 2.3. Flag missing common levers without insisting they be added.
5. Write the tactics to `00-map.md`.
6. Prioritise. `AskUserQuestion` has no rank widget, so present the tactics as a numbered list and ask the user to reply with their top 3 in order. Use `AskUserQuestion` (`multiSelect: true`, options capped at 4) only if you want to surface which to *include* in the priority set before ranking. Take the top 3 forward to keep Phase 5 tractable; tell the user the others are parked, not dropped.

### Phase 4 — Checkpoint: present the Mermaid tree

1. Generate a `graph LR` Mermaid diagram of the full tree, embedded as a fenced code block in `00-map.md`. Mark priority tactics with `:::priority`.
2. Present the diagram to the user: _"Here's the full map. Anything to revise before we go deep on the top-priority tactic? If not, we'll start Phase 5 with [tactic name]."_
3. If the user wants to revise, return to the relevant earlier phase. Do not collapse multiple revisions into one turn.

### Phase 5 — Per-tactic deep-dive

Create `01-<tactic-slug>.md` in the project folder for the top-priority tactic. Each later tactic gets `02-…`, `03-…`. Work through 5a, 5b, 5c in order; do not collapse them.

#### Phase 5a — If-then-because hypothesis statement

Load `references/pattern-library.md` section 2.4 and the Phase 5a reject criteria in `references/pushback-rules.md`.

1. Draft an if-then-because statement for the tactic, drawing on the strong example in section 2.4. Show the draft to the user as a starting point, not a final answer.
2. Discuss and refine. Check against the Phase 5a criteria: specific X; measurable Y with direction (add magnitude only if there's grounds for one, e.g. an analogue, prior test, or baseline); Y is a proximate metric (not LTV or annual retention); 2 or more distinct because-clauses (2–5 is normal, more isn't better); falsifiable; no conflated assumptions; no solution-in-disguise clauses; cohort specified.
3. Write the final statement to `01-<tactic-slug>.md`.

#### Phase 5b — Assumption list

Load `references/pattern-library.md` Part 3 (assumption sets by tactic type) and the Phase 5b reject criteria in `references/pushback-rules.md`.

1. Identify which tactic type from Part 3 best matches: discovery/findability, on-content engagement, off-platform touchpoint, new value proposition, onboarding/activation, or other. If "other", build a custom set from the seven assumption types in section 1.4 (problem, root-cause, desirability, mechanism, magnitude, value-chain, strategic/scope).
2. Propose the typical assumption set for that tactic type (usually 5–10 assumptions), each tagged by type. Propose more than you expect the user to keep. Where the tactic has multiple plausible solution routes (different surfaces, build-vs-iterate, narrow-vs-broad), make sure at least one *strategic / scope* assumption is in the proposed set — these are commonly skipped but kill tactics if wrong.
3. Present the list via `AskUserQuestion` (`multiSelect: true`) so the user picks which to keep. If you have more than 4 assumptions, split across two calls grouped sensibly (e.g. problem/root-cause/desirability in one, mechanism/magnitude/value-chain/scope in another). Follow with one open-prose turn for additions.
4. Run the LOFA kill-test on *every* assumption that survives. Don't ask the user "which 1–2 are LOFAs?" — that biases toward identifying too few. Instead, for each assumption in turn, run the test in section 1.11: *"If this turned out to be wrong, would the whole tactic die, or would only some solutions within it die?"* Three outcomes:
   - **Whole tactic dies → LOFA.** Mark it.
   - **One solution path dies but other paths survive → "important, not LOFA".** Mark it as load-bearing for the affected path only, not the tactic.
   - **Tactic survives with minor adjustment → not load-bearing.** Standard assumption.

   On first mention in any session, explain LOFA inline: _"Quick gloss: LOFA = Leap of Faith Assumption. The kind that kills the whole tactic if it's wrong, not just one solution within it. Lean-startup vocabulary; useful shorthand once you're using it."_ The kill-test produces however many LOFAs the tactic actually has — could be one, could be four. Don't cap.
5. Check against Phase 5b reject criteria: at least 5 assumptions, at least one root-cause and one value-chain, scope assumption present if the tactic has multiple solution routes, not all of one type, each labelled by type, LOFAs identified via the kill-test, all genuinely uncertain (cite-as-evidence things that are already known), not all feasibility-flavoured (the Cagan trap from section 1.5).

   Apply the soft check for the tactic type. For off-platform touchpoint tactics, check explicitly for the "touchpoint causally drives return visits, not just correlates" value-chain assumption — it is almost universally skipped. For discovery / findability tactics, check that the scope assumption (which surface to intervene on) is present.

#### Phase 5c — Confidence ratings

Load Phase 5c reject criteria in `references/pushback-rules.md` and section 1.9 of `references/pattern-library.md`.

1. For each assumption, ask the user to rate evidence as High / Medium / Low / None using `AskUserQuestion` (`multiSelect: false`, four options). Batch up to 4 assumptions in a single call (one question per assumption, within the 4-question cap). For longer assumption lists, run a second call.
2. **For each High *and* each Medium, ask the user to cite the evidence in one sentence.** This is where the skill earns its keep — Medium is the rating people give when they want to feel comfortable without justifying it. The citation doesn't need to be deep; it just needs to name the source (a specific report, dataset, prior test, industry analogue). Push back if "team agrees", "we just know", or "industry consensus" is offered without a source. Example: "Team alignment isn't evidence, it's a shared prior. What's the data, research, or analogous case behind it? If there isn't a specific one, this is better rated Low." If no citation can be produced, downgrade the rating: Medium → Low; High → Medium (and then re-ask for evidence).
3. For value-chain assumptions rated High *or* Medium, require causal-leaning evidence (matched-pair, propensity-matched, quasi-experimental, or strong analogous case). Raw correlations don't qualify (see section 5.7). Without that, value-chain assumptions cap at Low.
4. When a user rates an assumption higher than they earlier flagged it as a concern, pause. Ask explicitly: _"You mentioned earlier this might be a weakness — what changed? Or does this rating mean something narrower (e.g. 'works for engaged users but uncertain for this cohort')?"_ Log whichever they say. Don't let an earlier-flagged concern silently become "Medium = fine".
5. Apply the distribution soft check. If 80%+ are High, ask: _"That's a lot of high confidence for new work. Which would you say is the one you're least sure about?"_
6. Write the assumption list — with types, LOFAs (from the kill-test in 5b), confidence ratings, and evidence citations — to `01-<tactic-slug>.md`. Every High and Medium row must have an evidence citation; assumptions without citations get written at Low.

### Phase 6 — Experiment design

Load `references/pattern-library.md` sections 1.6 through 1.11 and the Phase 6 reject criteria in `references/pushback-rules.md`.

1. **Sort assumptions for testing by importance and confidence, in this order:**
   1. Low- or no-confidence LOFAs (from Phase 5b's kill-test). All of them, ordered by where they sit in the causal chain — the most upstream one first (no point testing "does X convert to Y" if "is X even possible" hasn't been resolved).
   2. Low-confidence non-LOFA assumptions that are still load-bearing for one solution route.
   3. Assumptions that inform implementation (e.g. *strategic / scope* questions like which surface to test on, or design questions like narrow-vs-broad).
   4. High-confidence assumptions: usually leave alone. Low-importance assumptions: not worth the test.

   Write this priority list out *before* drafting any experiments. The list goes into the doc as the opening of the Phase 6 section so a stakeholder reading cold sees the ranking before the methods.

2. **Draft experiments in priority order, not invention order.** The first experiment drafted is the test for the highest-priority assumption (usually the most upstream LOFA). Don't draft a Wave 2 / 3 / later experiment until the earlier ones are written. If you find yourself reaching for a downstream experiment first because it's easier to picture, that's a signal you should test the upstream assumption more cheaply first.

3. **Use stable experiment IDs tied to the assumption being tested, not sequential numbers.** Format: *Exp-<assumption-letter>-<n>* — e.g. *Exp-F-1* tests assumption F, *Exp-B-1* tests assumption B. If multiple experiments test the same assumption, use Exp-F-1, Exp-F-2, etc. This means reordering the experiment plan doesn't break references downstream. Group experiments into *waves* (e.g. Wave 1 = retrospective data work, Wave 2 = light in-product, Wave 3 = full test) by cost, not by assumption. Each wave can contain experiments testing several different assumptions.

4. For each experiment, propose the cheapest method that could falsify the assumption, drawing from the assumption-to-experiment matrix in section 1.8 and the validation methods matrix in section 1.7. Sequence cheapest-first; gate later expensive tests on earlier cheap ones.

5. Draft for each experiment:
   - **ID and assumption tested** (e.g. *Exp-F-1, tests F*)
   - **What we want to learn** (one or two specific questions, plain English)
   - **Method** (the cheapest viable)
   - **Success threshold** (numeric where possible, otherwise direction with magnitude)
   - **Decision criteria**: _"If X, we will Y. If Z, we will W."_ (Section 1.10 — experiments inform decisions, they are not decisions.)

6. **Identify where stage gates sit.** A stage gate goes immediately after the experiment(s) that test a LOFA. Don't place a stage gate where there is no LOFA test sitting above it — that's a gate with nothing to gate on. If multiple LOFAs are tested in one wave, the gate evaluates all of them together. Each gate names: what it's deciding, the success criteria for green/yellow/red, and what happens at each colour.

7. **Split gating experiments from implementation-design experiments.** Assumptions tagged *strategic / scope* or design-flavoured (e.g. narrow-vs-broad routing rules) inform *how* the next build is shaped, not *whether* to build. These go into a separate "Pre-build analysis" section that runs only after the relevant stage gate is green. Don't put implementation-design work into the gating waves — it wastes effort if the tactic dies at a LOFA.

8. Apply the cost-of-failure soft check before settling on fidelity: _"If we ran this tactic at full scale and the assumption turned out wrong, what would it cost to roll back? What's the brand or customer impact?"_ Use the answer to calibrate. Cheap-and-reversible tactics deserve cheap tests; irreversible decisions deserve test-flight-level rigour (section 1.6).

9. Check against Phase 6 reject criteria: priority list written first, experiments drafted in priority order, stable IDs used, cheapest test first, method matches assumption type, explicit decision criteria, fidelity matches cost of failure, success threshold specified, sequenced not parallel-build, stage gates placed only where LOFA tests sit, implementation-design work separated from gating work.

10. Write the experiment plan to `01-<tactic-slug>.md`, sequenced, with a "Next steps" section naming who would run each experiment.

### Phase 7 — Stakeholder polish and handoff

#### 7a — Stakeholder polish

Before reading back the doc, do a polish pass. The artefact at this point typically reads like a working doc (internal vocabulary, phase labels, jargon). A stakeholder seeing it cold will struggle. The fix isn't optional.

Apply these in order:

1. **Strip internal scaffolding from headings.** Remove "Phase 5a / 5b / 5c / 6" labels; replace with content-based names (*Hypothesis*, *Assumptions*, *Confidence and evidence*, *Experiments*). Phase numbers are framework metadata, not stakeholder content.

2. **Gloss every imported term on first use *in the final doc*, not just on first use in the conversation.** LOFA, root-cause assumption, value-chain assumption, scope assumption, the Cagan trap, horse-race ladder, counter-prior. The conversation gloss doesn't carry into the doc; a stakeholder reading the doc cold doesn't have it. Add a one-sentence plain-English gloss the first time each term appears in the *artefact*.

3. **Replace internal jargon with plain English where it doesn't earn its keep.** Examples to watch for: *counter-prior* → *evidence pointing the other way*; *load-bearing* → use sparingly, prefer plainer phrasing like *the one that decides everything*; *direct counter-prior* → just *counter-prior* with gloss, or *direct evidence against this*. Keep technical terms where they're load-bearing (LOFA itself, the assumption-type names) but always with first-use gloss.

4. **Open each major section with the point, not the framework.** Experiment sections in particular should open with "the priority of assumptions to test" or "here's how we'll test in order of cost", not a wave-by-wave explanation. Stakeholders want to know what's load-bearing, then how the test sequence supports it.

5. **Anti-AI-writing pass.** Run the checks in the humanizer guide (or equivalent): drop em-dash overuse, drop the rule-of-three padding, drop forced parallelism, prefer active voice, drop "AI vocabulary" words (delve, leverage, ensure, navigate, etc.), drop sycophantic openers ("Great question!"), drop chatbot artefacts ("Hope this helps"). Vary sentence length. The skill's output style influences how the user pitches the work — it should sound like a sharp human, not a templated artefact.

6. **Consistent cohort and entity naming.** Pick one form ("cool/cold subscribers", "casual subscribers", etc.) and use it throughout. Inconsistency triggers stakeholder confusion about whether different terms mean different things.

7. **Surface any deferred items in one place.** "Open items to chase before Wave 1 starts" or similar — a short list at the end of the Confidence section. Resolves what's known, what's not, and what needs chasing before any spend.

If a humanizer skill (or equivalent) is available in the environment, invoke it on the per-tactic doc as the final step of 7a. If not, apply the checks above manually.

#### 7b — Handoff conversation

1. Present the polished `01-<tactic-slug>.md` in full. Read back the hypothesis statement, the LOFAs (named individually, not just "the LOFAs"), the first experiment, and its decision criteria.
2. Ask whether to continue with the next priority tactic now or end the session.
3. If continuing, return to Phase 5 with the next tactic. The new file is `02-<tactic-slug>.md`, then `03-…`. Each new tactic doc gets its own 7a polish pass at the end.
4. When all priority tactics are done, or the user ends, summarise what's in `./strategic-experiments/<question-slug>/` and stop. Do not propose next steps the user did not ask for.

## Terminal state

The session ends when one of these is true:

- All priority tactics from Phase 3 have a per-tactic doc (`01-…`, `02-…`, `03-…`) that includes a hypothesis statement, typed assumption list with LOFAs marked, confidence ratings with evidence, and a sequenced experiment plan with decision criteria.
- The user ends the session early. In that case, the running docs are still left in a coherent state: `00-map.md` reflects the latest tree; any partially-finished per-tactic doc has a clear "in progress" marker at the top.

A successful session is one the user can hand to a colleague without explaining over Slack.
