# Changelog

## v0.3.1 — 2026-05-20

Refinements from the first sustained PM-driven use of the skill (cool/cold subscriber discovery tactic). All changes below address skill gaps that the PM had to push back on rather than the skill catching itself.

- **Seventh assumption type added: *strategic / scope*.** Surface choice, build-vs-iterate, narrow-vs-broad-scope decisions are common in discovery and value-prop tactics and kill tactics if wrong. Previously absent from the six-type list (1.4), so the skill systematically missed surface-choice questions. Now first-class.
- **LOFA identification tightened from "pick 1–2" to per-assumption kill-test.** Old wording biased toward identifying too few LOFAs. Phase 5b step 4 now runs the kill-test (from pattern-library 1.11) on every assumption in turn, with three possible outcomes (LOFA / load-bearing for one path / standard). Tactics with three or four LOFAs are now expected, not unusual.
- **LOFA chain ordering.** When multiple LOFAs are identified, the skill writes their dependency chain order in the doc (e.g. F → B → G in a discovery tactic). The test sequence must follow chain order, not just cost order. New soft check in Phase 6 pushback rules.
- **Medium confidence now requires evidence citation.** Previously only High needed a cite. Medium without a source is the rating people give when they want to feel comfortable without committing. Phase 5c step 2 now requires a one-sentence citation for Medium too; without one, the rating drops. New reject criterion in Phase 5c.
- **Contradiction check on confidence ratings.** If the user rates an assumption higher than they earlier flagged it as a concern, the skill pauses and asks what changed. Stops earlier-flagged concerns from silently becoming "Medium = fine".
- **Stable experiment IDs.** Sequential numbering (1.1, 1.2, 1.3…) breaks every reference when the plan is reordered. New format: *Exp-<assumption-letter>-<n>* (e.g. *Exp-F-1*, *Exp-B-1*, *PB-I-1*). Wave grouping by cost remains; experiment IDs are tied to the assumption being tested.
- **Experiment drafting must go in priority order, not invention order.** Phase 6 step 2 now requires the priority list of assumptions to be written *first*, then experiments drafted top-down. New reject criterion catches drafting downstream LOFA tests before upstream ones.
- **Stage gates only sit where LOFA tests precede them.** Previously gates could end up after non-LOFA work. New criterion forces gate placement to follow LOFA test placement.
- **Gating work vs implementation-design work separated.** Scope and design-input assumptions (e.g. narrow-vs-broad routing) go into a *Pre-build analysis* section that runs only after gating LOFAs are green. Stops implementation pre-work from being wasted when the tactic dies at a LOFA.
- **Phase 7 expanded with a stakeholder-polish pass (7a).** Stripping phase labels, glossing imported terms (LOFA, counter-prior, etc.) on first use *in the artefact*, removing internal jargon, anti-AI-writing pass, consistent cohort naming. The conversation gloss doesn't carry into the doc; a stakeholder reading cold needs the doc to gloss itself.
- **Pattern library 3.1 (discovery tactics) rewritten.** Headroom (magnitude) and surface-choice (strategic / scope) added as default LOFAs. Spike-trigger-and-trajectory analysis and discovery-path comparison added as default cheap experiment designs for the LOFA tests.

## v0.3 — 2026-05-19 (unreleased on main)

- Example rebalance and rule loosening across the pattern library and pushback rules.
- AskUserQuestion wiring throughout the phase orchestration.
- Loosened Phase 5a magnitude and because-clause count rules; added the precision principle; removed em dashes throughout pushback-rules.

## v0.1 — 2026-05-19

- Initial release. Eight-phase skill (Phase 0 entry triage through Phase 7 handoff) for decomposing strategic goals into testable hypotheses.
- Pattern library covers engagement and retention product domains, with worked examples from retail marketing and content subscription products.
- Pushback rules codified for Phases 1, 2, 3, 5a, 5b, 5c, and 6.
- Mermaid `graph LR` convention for the tree map; Graphviz `digraph` for the internal process flow.

## Future versions

Track changes here as the skill evolves.
