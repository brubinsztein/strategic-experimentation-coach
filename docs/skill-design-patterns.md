# Strategic Experimentation Skill: Design Patterns & Interaction Conventions

**Version:** 0.2
**Status:** Reference. Decisions locked for v0.1 of the skill; iterate as the skill is used.
**Purpose:** Captures the design and interaction patterns the skill follows. Read alongside `pattern-library.md` (domain content) and `pushback-rules.md` (reject criteria).

## Changelog

- **v0.2** — Converted "open questions" section to "decisions made" (all seven settled). Added the humanizer skill as a recommended companion for writing quality.
- **v0.1** — Initial draft synthesised from research on existing Claude skills.

---

## How this document is organised

Three sections:

1. **Format and structure conventions** — how skill files are organised
2. **Interaction patterns** — how the skill talks to the PM
3. **Specific design decisions** — where the skill deviates from defaults and why

---

# Part 1: Format and structure conventions

Drawn from Anthropic's official skill authoring docs and the canonical examples (`skill-creator`, `superpowers/brainstorming`, `frontend-design`).

## 1.1 File structure

```
strategic-experimentation-coach/
├── SKILL.md                          (required, <500 lines)
├── references/                       (loaded on demand)
│   ├── pattern-library.md
│   ├── pushback-rules.md
│   ├── question-patterns.md          (extracted subset for Phase 1-3)
│   ├── assumption-patterns.md        (extracted subset for Phase 5)
│   └── experiment-patterns.md        (extracted subset for Phase 6)
└── assets/
    └── running-doc-template.md       (starter template for 00-map.md)
```

The pattern library is too long to load fully each session. SKILL.md contains only phase orchestration, the conversation contract, and pointers. Phase-specific content lives in the references and gets loaded on demand.

## 1.2 YAML frontmatter

```yaml
---
name: strategic-experimentation-coach
description: <see Part 3 for the full text>
---
```

Conventions:
- Name: kebab-case, lowercase, no spaces.
- Description: third-person, explicit about *what* and *when*. Anthropic recommends being "pushy" with descriptions because Claude tends to under-trigger skills. Multiple specific trigger phrases beats one general description.

## 1.3 SKILL.md body conventions

- Length under 500 lines, body under 2000 words.
- Imperative voice ("Ask one question at a time", not "You should ask...").
- Lean SKILL.md → progressive disclosure to reference files. SKILL.md tells the model *which reference to load when*, not the content of those references.
- Examples beat abstractions. Pair each rule with a concrete example.
- Avoid all-caps MUST/NEVER/ALWAYS unless genuinely fragile. Explain *why* so the model can generalise to unanticipated cases. Anthropic's own skill-creator flags all-caps imperatives as a yellow flag.
- Use numbered checklists for sequenced workflows.
- Include a process flow diagram in Graphviz `digraph` syntax for skills with non-trivial control flow.

## 1.4 What goes where

SKILL.md contains:
- Phase orchestration (the checklist of phases, in order)
- Process flow diagram
- Core conversation contract
- Entry triage logic (Phase 0 routing)
- Pointers to references with explicit "load this when..." triggers
- Running doc location and format

References contain:
- Domain patterns by phase (loaded only when in that phase)
- Detailed reject criteria
- Long examples and worked cases
- Reference content the model uses for proposing options

---

# Part 2: Interaction patterns

From obra/superpowers `brainstorming` (the canonical example), Anthropic's `skill-creator`, and existing PM/discovery skills.

## 2.1 One question at a time

The single most consistent pattern across well-designed elicitation skills. Reasoning: multiple questions overwhelm the user; the answer to question 1 often changes question 2; the model adapts better with progressive information.

The skill never asks more than one question per turn, even when it thinks it knows the next two.

## 2.2 Multiple choice over open-ended where possible

Multiple choice is faster for the user and surfaces options they might not have considered. Use the `ask_user_input_v0` tool where available (mobile-friendly tappable options). Open-ended is fine for genuinely creative inputs.

Multiple choice fits at:
- Phase 0 entry triage
- Phase 3 tactic prioritisation (rank_priorities)
- Phase 5b assumption type labelling
- Phase 5c confidence ratings

Open-ended fits at:
- Phase 1 theoretical question
- Phase 2 strategic hypotheses
- Phase 5a hypothesis restatement

The skill should *propose* options as part of the question even when the user answers in prose.

## 2.3 Propose, don't just elicit

Weak elicitation: *"What are your strategic hypotheses?"* — user stares at a blank page.

Strong elicitation: *"Based on your question, here are 4 strategic directions that often apply: [A, B, C, D]. Which resonate? Are there others you'd add?"*

The skill proposes options drawn from the pattern library, then lets the user accept, edit, add, or reject. This is the dominant mode for the skill — it leverages the pattern library as a "library of patterns the user can pick from."

## 2.4 Present designs in chunks, validate each

Long monolithic output is hard to digest and hard to disagree with. The superpowers brainstorming skill chunks design presentation into 200-300 word sections, asking *"does this section look right so far?"* after each.

For our skill: at major checkpoints (after each phase), present the updated running doc in chunks with per-chunk validation.

## 2.5 Anti-pattern: "this is too simple to need the framework"

The superpowers skill counters this with: *"Every project goes through this process. A todo list, a single-function utility, a config change — all of them. 'Simple' projects are where unexamined assumptions cause the most wasted work."*

For our skill, the equivalent is *"this is just a small optimisation, I don't need the full framework."* The skill should still walk through hypothesis restatement and assumption identification — even if the design can be short. The discipline catches the assumption hiding in plain sight.

(Pure A/B optimisation work — testing a copy variant or button colour — is a legitimate skip. The skill distinguishes this in Phase 0 entry triage. See `pattern-library.md` §1.12 on growth experiments vs optimisation.)

## 2.6 Living running doc

The skill maintains a markdown document the user can see at checkpoints. Three purposes: working memory the user can edit between sessions, audit trail of decisions and overrides, eventual deliverable.

Conventions (locked in v0.1):
- Location: `./strategic-experiments/<question-slug>/` (project-relative)
- Filenames: `00-map.md` for the overall tree, `01-<tactic>.md` for per-tactic deep-dives
- Updated after every phase, not continuously
- User can edit between phases — skill re-reads the file at start of each phase

## 2.7 Pushback delivery (codified in pushback-rules.md)

The interaction pattern for pushback:
1. Name the issue specifically.
2. Explain why it matters in one sentence.
3. Offer 2–3 reframes drawn from the pattern library.
4. Ask the user to choose, edit, or override.

Worth reiterating because this is the skill's signature interaction. Most other skills are accommodating; ours is constructively obstinate.

## 2.8 The "experimentation IS product management" framing

Borrowed from Longden: the skill should not present itself as "an extra step before product work." It should present itself as *"this is how product work is done."*

Tone implication: the skill never apologises for the discipline. No *"I know this is more work, but..."* or *"Bear with me, this will be worth it..."* That tone implies the discipline is an imposition. Treat the discipline as the default — the way good PMs work.

## 2.9 Active listening, not interrogation

The skill is a coach, not a checklist. When the user gives a partial or wandering answer, reflect back what was heard, ask a clarifying follow-up, and only move on when there's a usable answer. The pushback rules give permission to push back; this principle gives permission to *follow the thread* when the user surfaces something important.

## 2.10 Pacing and session length

Phase 5 (per-tactic assumption mapping and experiment design) is the most cognitively heavy. Doing three tactics back-to-back is too much for one sitting. Rule: one tactic at a time, with clean handoff. At the end of each tactic deep-dive: *"This tactic is documented. Continue with the next priority tactic now, or come back later?"*

## 2.11 Plain prose, no AI tells

The skill's conversational output and written artefacts follow plain-prose principles. Specifically, avoid the patterns identified by the [humanizer skill](https://github.com/blader/humanizer): significance inflation, AI vocabulary ("delve", "tapestry", "leverage"), em-dash overuse, rule of three, copula avoidance ("serves as" instead of "is"), negative parallelisms ("it's not just X, it's Y"), signposting announcements ("let's dive in"), sycophantic openers ("great question!"), generic conclusions ("the future looks bright"), and filler hedging.

The full pattern list is worth borrowing into the SKILL.md style guidance. See the build prompt for the curated subset most relevant to skill authoring.

---

# Part 3: Specific design decisions

Where the skill differs from existing patterns, and why.

## 3.1 Monolithic skill, not chained sub-skills

Existing PM skill marketplaces tend to break product discovery into smaller skills chained by a parent command. Our choice: monolithic. The value lives in *enforced sequencing and pushback discipline*, which a chained-skills approach loses at the seams. SKILL.md owns the orchestration.

## 3.2 Aggressive pushback, codified

Reject criteria are codified in `pushback-rules.md`. More rigorous than any existing skill found in research. The skill's pushback is first-class behaviour, not an afterthought. The build prompt explicitly points the model at pushback-rules.md at each phase.

## 3.3 Domain-tuned pattern library

The pattern library is tuned to engagement, retention, and content products. Trade-off: less useful for B2B SaaS, marketplaces, etc. Acceptable for v0.1; expand later.

## 3.4 Heavier on suggesting than eliciting

A lot of existing skills are pure interviewers. Our skill is a coach: it generates candidate hypotheses/tactics/assumptions from the pattern library and asks the user to choose, edit, or extend. The skill is willing to be wrong when proposing — better to propose 5 candidates the user rejects 3 of than to ask the user to generate from scratch.

## 3.5 The skill ends by handing off, not running

The skill produces an experiment *plan* — sequenced cheapest-first, with decision criteria. It does not run the experiments. A/B tests, user interviews, data analysis — all outside scope. Phase 6 produces a clean handoff artefact.

## 3.6 No automatic invocation of downstream skills

The superpowers brainstorming skill ends by invoking `writing-plans`. We don't have an equivalent downstream skill. Terminal state is the running doc; the skill stops at end of Phase 7 and tells the user what the artefacts are.

## 3.7 YAML description

```yaml
description: This skill should be used when a PM, product team, or anyone doing product work wants to break down a strategic goal or theoretical question into testable hypotheses, prioritise tactics, and design lightweight experiments before committing engineering effort. Use this skill whenever the user mentions wanting to "test", "experiment", "validate", "de-risk", "prioritise tactics", "map out our approach", "figure out what to build next", or asks how to move a metric, even if they don't explicitly use the words "experiment" or "hypothesis." Also use when the user has identified a theoretical question, strategy, or set of tactics and wants to take the next step toward action. The skill enforces the discipline of testing assumptions before solutions: it pushes back on weak hypotheses, surfaces skipped assumptions, and matches experiments to risks. Do NOT use for pure execution of an already-designed experiment, for general product strategy advice that doesn't involve testing assumptions, or for pure A/B test optimisation work that doesn't need the full framework.
```

(Roughly 900 characters, within the 1024-char standard cap.)

---

# Decisions for v0.1 (settled)

These were open questions in v0.1 of this doc; settled in v0.2.

| # | Question | Decision |
|---|---|---|
| 1 | Working doc location | **Project-relative**: `./strategic-experiments/<slug>/`. Portable across teams. |
| 2 | Returning users / existing docs | **Scan at entry**: at start of session, check `./strategic-experiments/` for existing folders. Offer the user (a) continue an existing piece of work, (b) start something new, (c) view/edit an existing tree. |
| 3 | Mermaid rendering target | **Embedded code fence** in `00-map.md`. Renders natively in Notion, GitHub, most viewers. No external SVG generation. |
| 4 | `ask_user_input_v0` availability | **Use when available, fall back gracefully**. The build prompt instructs the skill to detect tool availability and use prose questions when not. |
| 5 | Skill name | **`strategic-experimentation-coach`**. Borrowed "coach" framing from the friendly-but-firm posture; "strategic-experimentation" describes scope. |
| 6 | First-line announcement | **Yes, announce briefly** on first invocation in a session: one line naming the skill and what it'll do. After that, no repeated announcements. |
| 7 | TodoWrite-style task tracking | **Yes**. The skill creates TodoWrite tasks per phase at entry, marks complete as it progresses. Prevents losing place in long multi-phase conversations. |

---

# Notes for future iteration

- Once the skill is in use, the running docs become a corpus that could feed an evaluation set — useful for tuning pushback aggressiveness.
- A companion skill for *executing* experiments (e.g., `design-user-interview`, `design-ab-test`) would be a natural extension.
- The pattern library's "common skipped assumptions" notes could become explicit auto-fired prompts when the skill detects a matching tactic type.
- The humanizer skill (or its principles) could be invoked as a final pass on completed running docs to improve writing quality.
- Pattern library coverage will need to expand beyond engagement/retention for the skill to be useful across domains.
