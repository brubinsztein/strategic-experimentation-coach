# Changelog

## v1.3, 2026-06-29

**Sharper evidence-surfacing and leaner turns, from a trial run.** Three fixes drawn from a session where the coach designed a full test for an assumption the team had already validated, and where the coach's own turns ran longest.

- **Surface prior evidence before designing a test.** The Phase 0.5 "what's been tried" probe now asks wider than formal efforts on the exact cohort, covering prior, adjacent, and informal tests and any analogue that bears on the work. Added the `EVIDENCE-CHECK` reject criterion in pushback-rules Phase 6b: as each LOFA is named, ask whether evidence already settles it before routing a fresh MVT. This stops the coach building a test for an assumption a prior trial already validated.
- **Brevity applies to proposal turns, not only questions.** The conversation contract extends the two-sentence run-up cap to proposal turns, keeping exposition minimal and reserving length for the framework's structured statements. The coach's own turns are where verbosity creeps back.
- **Build cost visible while choosing.** New Phase 4 soft check in pushback-rules, with a matching line in pattern-library §2.4: where candidate solutions vary by channel or vehicle, name the rough build or infrastructure cost on each as it is proposed, so the cheap-to-build path is visible during selection rather than discovered after.

## v1.2, 2026-06-29

**Deeper probing and cleaner docs, from a trial run.** Two themes: make the coach probe instead of assume, and fix the quality of the written docs.

- **New Phase 0.5, Discovery and context.** Before any problem work, the coach probes for the product, the cohort and its operational definition, the metric and baseline, prior attempts, hard constraints, and the test/targeting capability. Added to the phase checklist and process-flow diagram.
- **Global product context file.** Context that holds across projects is saved once to `./strategic-experiments/product-context.md` and read at the start of every project. Documented in the README.
- **Probe, do not assume (conversation contract).** A new coaching principle: ask before filling gaps, state assumptions as assumptions, build decompositions with the user rather than handing over a finished tree, and interrogate buried causal claims before accepting a statement.
- **Active divergence at the problem layer.** Phase 3 replaces the weak coverage soft-check with an active divergence sweep across causal axes, done with the user, and adds the `EMBEDDED-CAUSE-UNPROBED` reject criterion. Added the funnel decomposition pattern to pattern-library §2.3 as a reusable trick.
- **Solution leanings probe (Phase 4).** The coach asks the user's leanings and exclusions before proposing solution candidates.
- **Test-capability probe (Phase 6).** Confirms targeting and control availability before beliefs and LOFAs, so a "no harm to other cohorts" belief is dropped when the change targets one cohort only. New `TEST-CAPABILITY` probe in pushback-rules.
- **Writing quality enforced across all docs.** Zero em-dashes and complete-sentence prose are now hard contract rules, and the humanizer/style pass runs on `00-map.md` at each checkpoint, not only on the per-solution doc at handoff. This closes the gap that let em-dashes and fragments survive in the map doc.
- **Readable diagram, no clutter.** The `:::priority` Mermaid class now sets an explicit dark text colour (`color:#1f2937`) so pale fills stay legible. The map diagram is restricted to Theory → Strategic → Problem(s) → Solution(s) with problem-to-sub-problem fan-out; LOFAs, gates, diagnoses, and MVTs are kept in prose. The map links to each per-solution doc.
- **Markdown solution statement.** The full-format statement is written into the doc as markdown with bold labels (**For**, **If**, **Then**, **Leading to**, **Without**), not inside a code block. Updated the pattern-library exemplars to match.
- **Template reworked.** New readable diagram, a single "What unblocks this, in order" section replacing the confusing "Next: data ask" block, a dedicated "Open gaps" section, a prose Notes block, and a per-solution docs links section.

## v1.1, 2026-06-26

**Lean, recommendation-first running doc.** Reordered the running-doc template to open with the recommendation and the tree, ahead of the question and hypotheses. Moved section guidance into HTML comments so it no longer bleeds into the written doc. Merged priority order into the solution list and replaced scattered italic side-notes with a single Notes block. Added a conversation-contract rule: write the doc as a lean artifact — plain-English wrapper (recommendation, data ask, notes), framework-precise hypotheses kept intact, no process labels, and self-contained folders with no cross-references to other projects.

## v1.0, 2026-06-26

**Extend onto the full six-level spine.** Set the spine to Theoretical question → Strategic hypothesis → Problem hypothesis → Solution hypothesis → MVT → validated/production solution, with a confidence gate at each step. The theoretical question and strategic hypothesis stay at portfolio altitude (the layers that select the project) and are skippable via Phase 0 triage, which now routes entry at any altitude. Inserted the problem hypothesis from the team model. Absorbed the old functional-hypothesis (tactic) layer into the problem hypothesis. Re-numbered phases: 0 triage, 1 theoretical question, 2 strategic hypotheses, 3 problem hypotheses, 4 solution hypotheses, 5 checkpoint, 6 per-solution deep-dive, 7 MVT design, 8 handoff. Adopted the richer hypothesis format: an explicit causal chain to the north-star via named intermediate steps, a mandatory guardrail clause, and inline confidence-plus-evidence-gap on every belief and LOFA, with beliefs and LOFAs kept as separate lists. Replaced the source-count confidence scale with HIGH (previous test + validated data) / MEDIUM (correlation, flagged not-causation) / LOW (anecdotal/vibes). Sharpened experiment design into MVT design (lowest-effort test that validates or kills a solution), with leading/lagging/guardrail metric tiers, learning-value prioritisation, the "kills N ideas at once" shared-assumption bonus, the "is there a lower-effort test for the same point?" check, and shared/upstream-LOFA detection. **Deferred:** the full MVT blueprint (test-construct detail, fidelity-floor specifics, sign-off mechanics) is flagged as a later pass, not specified now. Promoted the value-chain connection to a first-class gate, plus new pushback rules for vague beliefs, beliefs disconnected from the mechanism, and unisolated problems. Added a validation step: rewrite the weak source hypotheses with the new rules to confirm the pushback fires and to seed obfuscated before/after worked examples. New worked examples and pushback fixtures harvested (obfuscated) from real product hypothesis sets. Trimmed Phase 8 polish and repeated glosses for conciseness. Removed the project-specific "Day N" sequencing concept; kept only cost-based waves (Wave 1/2/3). Existing discipline retained: LOFA kill-test, evidence citation, value-chain causal-evidence rule, cheapest-test-first, stage gates, decision criteria.

## v0.3.1, 2026-05-20

Refinements from the first sustained PM-driven use of the skill (a light-engagement subscriber discovery tactic). All changes below address skill gaps that the PM had to push back on rather than the skill catching itself.

- **Seventh assumption type added: *strategic / scope*.** Surface choice, build-vs-iterate, narrow-vs-broad-scope decisions are common in discovery and value-prop tactics and kill tactics if wrong. Previously absent from the six-type list (1.4), so the skill systematically missed surface-choice questions. Now first-class.
- **LOFA identification tightened from "pick 1-2" to per-assumption kill-test.** Old wording biased toward identifying too few LOFAs. Phase 5b step 4 now runs the kill-test (from pattern-library 1.11) on every assumption in turn, with three possible outcomes (LOFA / load-bearing for one path / standard). Tactics with three or four LOFAs are now expected, not unusual.
- **LOFA chain ordering.** When multiple LOFAs are identified, the skill writes their dependency chain order in the doc (e.g. F → B → G in a discovery tactic). The test sequence must follow chain order, not just cost order. New soft check in Phase 6 pushback rules.
- **Medium confidence now requires evidence citation.** Previously only High needed a cite. Medium without a source is the rating people give when they want to feel comfortable without committing. Phase 5c step 2 now requires a one-sentence citation for Medium too; without one, the rating drops. New reject criterion in Phase 5c.
- **Contradiction check on confidence ratings.** If the user rates an assumption higher than they earlier flagged it as a concern, the skill pauses and asks what changed. Stops earlier-flagged concerns from silently becoming "Medium = fine".
- **Stable experiment IDs.** Sequential numbering (1.1, 1.2, 1.3…) breaks every reference when the plan is reordered. New format: *Exp-<assumption-letter>-<n>* (e.g. *Exp-F-1*, *Exp-B-1*, *PB-I-1*). Wave grouping by cost remains; experiment IDs are tied to the assumption being tested.
- **Experiment drafting must go in priority order, not invention order.** Phase 6 step 2 now requires the priority list of assumptions to be written *first*, then experiments drafted top-down. New reject criterion catches drafting downstream LOFA tests before upstream ones.
- **Stage gates only sit where LOFA tests precede them.** Previously gates could end up after non-LOFA work. New criterion forces gate placement to follow LOFA test placement.
- **Gating work vs implementation-design work separated.** Scope and design-input assumptions (e.g. narrow-vs-broad routing) go into a *Pre-build analysis* section that runs only after gating LOFAs are green. Stops implementation pre-work from being wasted when the tactic dies at a LOFA.
- **Phase 7 expanded with a stakeholder-polish pass (7a).** Stripping phase labels, glossing imported terms (LOFA, counter-prior, etc.) on first use *in the artefact*, removing internal jargon, anti-AI-writing pass, consistent cohort naming. The conversation gloss doesn't carry into the doc; a stakeholder reading cold needs the doc to gloss itself.
- **Pattern library 3.1 (discovery tactics) rewritten.** Headroom (magnitude) and surface-choice (strategic / scope) added as default LOFAs. Spike-trigger-and-trajectory analysis and discovery-path comparison added as default cheap experiment designs for the LOFA tests.

## v0.3, 2026-05-19 (unreleased on main)

- Example rebalance and rule loosening across the pattern library and pushback rules.
- AskUserQuestion wiring throughout the phase orchestration.
- Loosened Phase 5a magnitude and because-clause count rules; added the precision principle; removed em dashes throughout pushback-rules.

## v0.1, 2026-05-19

- Initial release. Eight-phase skill (Phase 0 entry triage through Phase 7 handoff) for decomposing strategic goals into testable hypotheses.
- Pattern library covers engagement and retention product domains, with worked examples from retail marketing and content subscription products.
- Pushback rules codified for Phases 1, 2, 3, 5a, 5b, 5c, and 6.
- Mermaid `graph LR` convention for the tree map; Graphviz `digraph` for the internal process flow.

## Future versions

Track changes here as the skill evolves.
