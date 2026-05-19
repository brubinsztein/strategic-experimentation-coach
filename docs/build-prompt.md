# Build Prompt: `strategic-experimentation-coach` skill

**Version:** 0.3
**Changes from v0.2:** Added requirements for publishing this skill as a public GitHub repository — README.md, LICENSE, CHANGELOG.md, installation instructions, attribution, and a `docs/` folder containing the methodology so others can fork and improve it.
**Changes from v0.1:** Added humanizer skill guidance to the style section and conversation contract.

Paste this into Claude Code (run from the directory containing the three reference documents) to build the skill.

---

## What you're building

A Claude skill called `strategic-experimentation-coach`, packaged as a self-contained public GitHub repository. The skill helps product managers decompose a strategic goal into testable hypotheses, prioritise tactics, and design lightweight experiments — before committing engineering effort. It enforces the discipline that PMs typically skip: testing assumptions before solutions, pushing back on weak hypotheses, surfacing skipped assumptions, and matching experiments to risks.

The skill is monolithic (one skill, internal phases) rather than chained sub-skills, because its value lives in the enforced sequencing and pushback discipline.

The repository will live at `github.com/brubinsztein/strategic-experimentation-coach` and be installable by anyone via `git clone`.

## Source materials

Three reference documents in this directory contain the substantive content. Read all three before starting:

1. **`pattern-library.md`** — domain content. The framework hierarchy (theoretical question → strategic hypothesis → functional hypothesis → solution → experiment), six assumption types, experiment ladder, validation methods matrix, common assumption sets by tactic type, anti-patterns. This is the model's reference for what good looks like and what to propose to users.

2. **`pushback-rules.md`** — codified reject criteria for each phase, with criterion / good example / bad example tables. This is the model's reference for what to reject and how.

3. **`skill-design-patterns.md`** — interaction conventions, structural decisions, format requirements. Read this for how the skill behaves (one question at a time, propose-don't-just-elicit, chunked presentation with sign-off, etc.).

## Repository structure to produce

```
strategic-experimentation-coach/         # repo root (also = skill folder when cloned)
├── README.md                            # public-facing project description
├── LICENSE                              # MIT
├── CHANGELOG.md                         # version history
├── SKILL.md                             # the skill itself (<500 lines)
├── references/                          # loaded by skill on demand
│   ├── pattern-library.md               # full domain reference
│   └── pushback-rules.md                # full reject criteria
├── assets/
│   └── running-doc-template.md          # template for 00-map.md
└── docs/                                # methodology, for contributors and forkers
    ├── skill-design-patterns.md         # design decisions and interaction conventions
    └── build-prompt.md                  # this build prompt (lets others rebuild/improve)
```

Design notes on the layout:

- The repo root IS the skill folder. When someone clones the repo into their Claude Code skills directory, the SKILL.md sits at the root where Claude Code expects it.
- `references/` contains two full reference docs the skill loads on demand. The skill points the model at specific sections of each rather than splitting into per-phase files (one source of truth is easier to maintain).
- `docs/` exists for humans reading the repo. Claude Code can technically see these files, but they don't fit the SKILL.md description, so they shouldn't get loaded inadvertently.
- `assets/` holds output templates (running-doc-template.md).

## YAML frontmatter

Use this frontmatter for SKILL.md (you may tighten the description if it's too long, but keep the explicit trigger phrases and the "do not use for" exclusion):

```yaml
---
name: strategic-experimentation-coach
description: This skill should be used when a PM, product team, or anyone doing product work wants to break down a strategic goal or theoretical question into testable hypotheses, prioritise tactics, and design lightweight experiments before committing engineering effort. Use this skill whenever the user mentions wanting to "test", "experiment", "validate", "de-risk", "prioritise tactics", "map out our approach", "figure out what to build next", or asks how to move a metric, even if they don't explicitly use the words "experiment" or "hypothesis." Also use when the user has identified a theoretical question, strategy, or set of tactics and wants to take the next step toward action. The skill enforces the discipline of testing assumptions before solutions: it pushes back on weak hypotheses, surfaces skipped assumptions, and matches experiments to risks. Do NOT use for pure execution of an already-designed experiment, for general product strategy advice that doesn't involve testing assumptions, or for pure A/B test optimisation work that doesn't need the full framework.
---
```

## What the skill does, phase by phase

The skill runs an eight-phase workflow (Phase 0 through Phase 7, where Phase 0 is entry triage). SKILL.md should orchestrate these as a numbered checklist, with TodoWrite tasks created at the start of each phase to track progress.

### Phase 0 — Entry triage and context scan

When the skill fires:

1. **Announce briefly** (one line): *"Activating strategic-experimentation-coach. I'll help you decompose this into testable hypotheses and design experiments. This goes in phases — push back at any point if something doesn't fit."*

2. **Scan for existing work.** Check for `./strategic-experiments/` directory. If it exists, list any sub-folders and ask the user (using `ask_user_input_v0` if available) whether to (a) continue an existing piece of work, (b) start something new, or (c) view/edit an existing tree.

3. **Triage the entry point.** If starting new, ask where the user is (`ask_user_input_v0` single_select):
   - *"I have a vague problem or goal — help me frame it"*
   - *"I have a theoretical question or strategy, help me break it down"*
   - *"I have tactics already, help me design experiments"*
   - *"I'm doing pure optimisation (A/B test on a known thing) — let me skip the framework"*

   Route to Phase 1, 2, 3, 5, or a fast-path respectively. If pure optimisation, run a stripped-down version with only Phase 5a (hypothesis statement) and Phase 6 (experiment design), and warn the user about the trade-off.

4. **For non-skipped paths**, create a project folder at `./strategic-experiments/<question-slug>/` and initialise `00-map.md` from the template in `assets/`.

### Phase 1 — Theoretical question

Load `references/pattern-library.md` (sections 2.1 and the Phase 1 reject criteria in `references/pushback-rules.md`).

1. Ask the user what their theoretical question is. *Don't* present a list — this is an open-generation moment.
2. Check the user's answer against the Phase 1 reject criteria. If it fails any criterion, push back per the rules: name the issue, explain why, offer 2–3 reframes from section 2.1 of pattern-library, ask the user to choose, edit, or override.
3. Once a usable theoretical question is in place, write it to `00-map.md` and confirm.

### Phase 2 — Strategic hypotheses

Load `references/pattern-library.md` (section 2.2) and the Phase 2 reject criteria.

1. Propose 3–5 candidate strategic hypotheses drawn from the patterns, tailored to the user's theoretical question type (engagement / acquisition / monetisation / etc.). Present them as a list.
2. Ask the user to accept, edit, add, or reject — open-ended response, not multiple choice.
3. Check the resulting set against Phase 2 reject criteria. Push back if needed.
4. Soft-check: are any contradictory hypotheses present? If not, prompt the user to consider the bet they're not currently considering.
5. Write the strategic hypotheses to `00-map.md` and present the updated tree.

### Phase 3 — Functional hypotheses (tactics)

Load `references/pattern-library.md` (section 2.3) and the Phase 3 reject criteria.

1. For each strategic hypothesis, propose 2–4 candidate functional hypotheses (tactics) drawn from the patterns. Present them under each parent hypothesis.
2. Ask the user to accept, edit, add, or reject. Open-ended.
3. Check against Phase 3 reject criteria (must be tactics not solutions, must ladder to parent, must be testable).
4. Soft-check coverage against the patterns library — flag if a common lever is missing.
5. Write the tactics to `00-map.md`.
6. **Prioritise.** Use `ask_user_input_v0` with `rank_priorities` to have the user rank the tactics. Limit to top 3 to keep Phase 5 tractable.

### Phase 4 — Checkpoint: present the Mermaid tree

1. Generate a Mermaid `graph LR` (left-to-right) diagram of the full tree, embedded as a fenced code block in `00-map.md`.
2. Present the diagram to the user with a checkpoint message: *"Here's the full map. Anything you want to revise before we go deep on the top-priority tactic? If not, we'll start Phase 5 with [tactic name]."*
3. Allow the user to loop back to any earlier phase if they want to revise.

### Phase 5 — Per-tactic deep-dive (one tactic at a time, with clean handoff)

For the top-priority tactic, create `01-<tactic-slug>.md` in the project folder. Then:

#### Phase 5a — Hypothesis restatement (if-then-because)

Load the Phase 5a section of pushback-rules and section 2.4 of pattern-library.

1. Draft an if-then-because hypothesis statement for the tactic. Show the draft to the user.
2. Refine through discussion. Check against Phase 5a reject criteria (specific X, measurable Y, falsifiable, multiple distinct because-clauses, no conflated assumptions, specifies cohort).
3. Write the final statement to `01-<tactic-slug>.md`.

#### Phase 5b — Assumption list

Load `references/pattern-library.md` (Part 3 — the assumption sets by tactic type).

1. Identify which tactic type from the patterns library best matches this tactic (discovery / on-content engagement / off-platform touchpoint / new value prop / onboarding / other).
2. Propose the typical assumption set for that tactic type — 5–10 assumptions, each labelled by type (problem / root-cause / desirability / mechanism / magnitude / value-chain).
3. Ask the user to confirm, edit, add, or remove assumptions. The skill should be willing to propose more than it accepts.
4. **Mark LOFAs.** Ask the user which 1–2 assumptions are load-bearing (if wrong, the whole tactic dies).
5. Check against Phase 5b reject criteria — at least 5 assumptions, must include root-cause and value-chain, must not all be one type, must label by type, must have LOFAs marked.

#### Phase 5c — Confidence ratings

1. For each assumption, ask the user to rate evidence as High / Medium / Low / None (`ask_user_input_v0` with single_select per assumption).
2. For each High rating, ask the user to cite the evidence — push back if "team agrees" is offered as evidence.
3. Check against Phase 5c reject criteria — not all High, evidence cited for Highs, distribution looks realistic.
4. Write the assumption list with types, LOFAs, confidence, and evidence citations to `01-<tactic-slug>.md`.

### Phase 6 — Experiment design

Load `references/pattern-library.md` (sections 1.6 through 1.11 — the experiment ladder, validation methods matrix, and experiment-to-assumption mapping).

1. Identify the assumptions to test: low- or no-confidence LOFAs first, then low-confidence high-importance non-LOFAs.
2. For each, propose the cheapest experiment that could falsify it, drawing from the experiment-to-assumption matrix. Sequence cheapest-first.
3. For each proposed experiment, draft:
   - The assumption it tests
   - The method (cheapest viable)
   - The success threshold (numeric where possible)
   - **Decision criteria**: *"If X, we will Y. If Z, we will W."*
4. **Cost-of-failure check.** Ask: *"If we ran this tactic at full scale and the assumption turned out wrong, what would it cost to roll back? What's the brand/customer impact?"* Use this to calibrate experiment fidelity.
5. Write the experiment plan, sequenced, to the per-tactic doc with a "Next steps" section naming who would run each experiment.

### Phase 7 — Handoff

1. Present the completed `01-<tactic-slug>.md`.
2. Ask whether to continue with the next priority tactic now or end the session.
3. If continuing, return to Phase 5 with the next tactic. Each tactic gets its own `02-`, `03-`, etc. file.
4. When all priority tactics are done (or the user ends the session), summarise what's in the project folder and stop.

## Conversation contract

Bake these into SKILL.md as non-negotiable behaviours:

- **One question per turn.** Never bundle questions, even when you think you know the next two. The user's answer to the first changes the second.
- **Propose before eliciting.** At every generative phase, the skill first proposes candidates from the patterns reference, then asks the user to accept, edit, add, or reject. Don't ask the user to generate from a blank page.
- **Multiple choice where possible.** Use `ask_user_input_v0` (with single_select, multi_select, or rank_priorities as appropriate) for phases where the user is choosing or ranking. Fall back to open prose questions when the tool isn't available. Use open prose for genuinely generative inputs (the theoretical question, strategic hypotheses, hypothesis restatement).
- **Chunk and validate.** When presenting longer output (the full tree, the assumption list, the experiment plan), break it into sections and ask after each whether it looks right so far.
- **Pushback before acceptance.** At each phase, check the user's input against the relevant pushback criteria *before* writing to the running doc. When pushing back: name the issue specifically, explain why it matters in one sentence, offer 2–3 reframes, ask the user to choose, edit, or override.
- **Overrides are logged.** When the user overrides a pushback, log it in the running doc in the format specified by pushback-rules.md. Don't refuse to proceed.
- **Active listening over rigid script.** If the user surfaces something important that wasn't anticipated, follow the thread before returning to the script.
- **Don't apologise for the discipline.** Never frame the work as "more work" or "bear with me." This is how good product work is done.
- **Plain prose, no AI tells.** The skill's conversational output and the artefacts it writes follow plain-prose principles. Avoid the patterns listed in the style guidance section below: significance inflation, AI vocabulary, em-dash overuse, rule of three, signposting, sycophancy, generic conclusions, filler hedging.
- **Use TodoWrite (or equivalent task tracking) to track phase progress.** Create tasks at the start of each phase, mark complete as you go.

## Running doc format

The skill maintains markdown files under `./strategic-experiments/<question-slug>/` (project-relative):

- `00-map.md` — the full tree, with an embedded Mermaid diagram. Updated after each phase 1–4.
- `01-<tactic-slug>.md`, `02-<tactic-slug>.md`, etc. — per-tactic deep-dives.

The skill re-reads these files at the start of each phase rather than relying on conversation memory.

Provide a template for `00-map.md` in `assets/running-doc-template.md`. Include placeholder sections for the theoretical question, strategic hypotheses, tactics, Mermaid diagram, and a decision log.

## Mermaid diagram convention

Use `graph LR` (left-to-right) layout. Mark priority tactics with a `:::priority` class. Embed as a fenced code block in `00-map.md`.

## SKILL.md content guide

SKILL.md should contain, in this order:

1. YAML frontmatter (exact text above)
2. Skill purpose (2-3 sentences)
3. The anti-pattern this skill counters (a paragraph using Longden's framing)
4. Conversation contract (the non-negotiable behaviours)
5. Phase checklist (numbered list)
6. Process flow diagram in Graphviz `digraph` syntax
7. Per-phase orchestration with explicit "load reference X" pointers
8. Terminal state — what "done" looks like

Keep SKILL.md under 500 lines. Detailed content lives in `references/`.

## Style guidance for SKILL.md prose

The SKILL.md gets read by the model running the skill. The patterns it gets surrounded by influence the patterns it produces in conversation. The SKILL.md itself should be written in plain prose, not the AI-tinged style models default to.

### Core principles

- **Imperative voice**, addressed to the model running the skill ("Ask one question at a time", not "You should ask..." or "Claude should...").
- **Concrete examples** beat abstract principles. Where you give a rule, follow it with an example of input and reaction.
- **Avoid all-caps MUST/NEVER/ALWAYS** unless the step is genuinely fragile. Explain the *why* so the model can generalise to cases the skill didn't anticipate.
- **Default assumption: the model is smart.** Only add context the model doesn't already have.

### Avoiding AI tells

Drawn from the [humanizer skill](https://github.com/blader/humanizer) (based on Wikipedia's "Signs of AI writing"). These patterns make prose feel mechanical. Avoid in both the SKILL.md itself and in the skill's conversational output:

- **Significance inflation**: "pivotal moment", "groundbreaking", "transformative", "seamless", "robust". State things plainly.
- **AI vocabulary**: "delve", "tapestry", "landscape", "navigate", "leverage", "showcase", "testament to", "ensure", "facilitate". Use plainer words.
- **Copula avoidance**: "serves as", "features", "boasts". Use "is" or "has".
- **Rule of three**: forced triplets for rhythm ("innovation, inspiration, and insights"). Use the natural number of items.
- **Negative parallelisms**: "It's not just X, it's Y". State the point directly.
- **Em-dash overuse**: many em-dashes per page. Mostly use commas or periods.
- **Bold overuse**: every other phrase bolded. Bold only when genuinely necessary.
- **Synonym cycling**: switching terms for the same thing. Pick one.
- **Signposting announcements**: "Let's dive in", "Here's what you need to know". Just start.
- **Sycophantic tone**: "Great question!", "Absolutely right!". Skip the flattery.
- **Generic conclusions**: "The future looks bright". Be specific or skip.
- **Chatbot artifacts**: "I hope this helps", "Let me know if you need anything else". Remove entirely.
- **Filler phrases**: "In order to" → "To". "Due to the fact that" → "Because". "It's worth noting that" → just say the thing.
- **Vague attributions**: "Experts say...", "Research shows...". Either cite a source or drop the claim.
- **Inflated -ing phrases**: "showcasing the power of...", "highlighting the importance of...". Mostly noise; cut.

### Final pass

After drafting the SKILL.md and README.md, run them through one of these:

- If the [humanizer skill](https://github.com/blader/humanizer) is available, invoke it and apply suggested edits where they don't change meaning.
- If not, manually scan against the list above.

Re-read the draft aloud (or imagine doing so). Sentences that sound stilted or like marketing copy probably contain AI tells.

## Public repository content

The repo is going on GitHub at `github.com/brubinsztein/strategic-experimentation-coach`. The following files need to be produced at the repo root.

### README.md

Aim for something a developer or PM can read in 2 minutes and decide whether to install. Structure:

```markdown
# Strategic Experimentation Coach

> A Claude skill that helps product managers decompose strategic goals into testable hypotheses, prioritise tactics, and design lightweight experiments — with pushback discipline baked in.

[1-paragraph what-and-why. Explain the problem (PMs jump to solutions before testing assumptions), what the skill does (enforces the decomposition discipline), and who it's for (PMs, product teams, founders).]

## What it does

[Brief overview of the 7-phase workflow. Use a bullet list or a short table. Don't overload with detail — link to the SKILL.md for the spec.]

The skill produces a project folder at `./strategic-experiments/<question-slug>/` containing a tree map (`00-map.md`) and per-tactic deep-dives (`01-...`, `02-...`). Each per-tactic doc ends with a sequenced experiment plan.

## Installation

### Claude Code

​```bash
mkdir -p ~/.claude/skills
git clone https://github.com/brubinsztein/strategic-experimentation-coach.git ~/.claude/skills/strategic-experimentation-coach
​```

### Claude.ai

[If applicable for the user's environment — instructions to upload as a custom skill. If you're not sure how this works in claude.ai, link to Anthropic's skill upload docs.]

## Usage

Once installed, the skill triggers automatically when you ask Claude things like:

- *"Help me figure out how to grow engagement among casual users."*
- *"I have a theoretical question I want to break down into experiments."*
- *"How should we test whether better content discovery would help retention?"*

Or invoke it directly:

​```
/strategic-experimentation-coach
​```

## How it works

[A short section explaining: the SKILL.md orchestrates phases, references/ contains domain patterns and reject criteria the skill loads on demand, the running docs are markdown files the user can edit between sessions.]

## Frameworks this synthesises

This skill stands on the shoulders of several established product discovery and growth experimentation frameworks:

- **Marty Cagan / SVPG (INSPIRED)** — the four product risks
- **Teresa Torres (Continuous Discovery Habits)** — opportunity solution trees, assumption mapping
- **David Bland & Alex Osterwalder (Testing Business Ideas)** — the experiment library
- **Itamar Gilad (Evidence Guided / GIST)** — the confidence meter
- **Jonny Longden / Speero (The Apollo Principle, XOS)** — the theoretical-question → strategic-hypothesis → functional-hypothesis hierarchy

See `docs/skill-design-patterns.md` for how these are synthesised.

## Contributing

Issues and PRs welcome. The skill is v0.1 and expected to evolve.

If you want to extend the pattern library for a different domain (B2B SaaS, marketplaces, e-commerce), the simplest path is to add a new section to `references/pattern-library.md` Part 3 with the typical assumption sets for your domain, and add domain-specific anti-patterns to Part 5. Send a PR.

If you want to fork the methodology to build a different coaching skill, see `docs/build-prompt.md` — it's the prompt that produced this skill.

## License

MIT. See [LICENSE](LICENSE).

## Credits

Built by [@brubinsztein](https://github.com/brubinsztein). Skill format follows [Anthropic's Agent Skills standard](https://github.com/anthropics/skills). Writing-quality pass uses principles from the [humanizer skill](https://github.com/blader/humanizer).
```

A few notes on the README:

- Don't apologise or hedge — the README should read as confident about the skill's value.
- The "What it does" section is the hook — get it right. A short bullet list of the phases is fine; don't reproduce the whole spec.
- Apply the same plain-prose principles to the README as to SKILL.md. AI-tinged READMEs are very obvious.
- Include a screenshot or sample transcript if you can produce one. Even a code-fenced snippet of "here's what a session looks like" helps.

### LICENSE

Standard MIT license. Generate the full text using GitHub's MIT license template with:

- Year: `2026` (or current year)
- Copyright holder: `Benjamin Rubinsztein`

If you don't have access to a template, use the standard MIT text — readily available at [opensource.org/license/mit](https://opensource.org/license/mit).

### CHANGELOG.md

Keep it lightweight. Format:

```markdown
# Changelog

## v0.1 — [date]
- Initial release. Seven-phase skill (entry triage through experiment handoff) for decomposing strategic goals into testable hypotheses.
- Pattern library covers engagement/retention product domains.
- Pushback rules codified for phases 1–6.

## Future versions
Track changes here as the skill evolves.
```

### docs/ folder content

Copy these source files unchanged into `docs/`:

- `docs/skill-design-patterns.md` — copy from the build directory's `skill-design-patterns.md`.
- `docs/build-prompt.md` — copy from the build directory's `build-prompt.md` (this file).

These are for transparency and to let others fork the methodology. Don't ship `pattern-library.md` or `pushback-rules.md` into `docs/` — they're already in `references/` and will get edited as the skill evolves.

## Acceptance criteria

Before considering the repo complete, verify:

### The skill itself

- [ ] SKILL.md is under 500 lines (~2000 words)
- [ ] YAML frontmatter has `name` and `description` as specified
- [ ] Description includes explicit trigger phrases beyond just "experiment" and "hypothesis"
- [ ] All seven phases (plus Phase 0 entry triage) are orchestrated explicitly in SKILL.md
- [ ] Each phase has an explicit "load reference X" pointer
- [ ] Pushback discipline is referenced at every relevant phase
- [ ] Process flow diagram is included
- [ ] Reference files exist in `references/` and contain the appropriate content
- [ ] Mermaid convention is documented
- [ ] Running doc template exists in `assets/`
- [ ] No all-caps MUST/NEVER/ALWAYS without explanation
- [ ] Examples are concrete, not abstract
- [ ] The skill announces itself on first invocation
- [ ] Use of `ask_user_input_v0` is conditional on availability with fallback
- [ ] Project-relative folder (`./strategic-experiments/`) is used for the running docs

### The repository

- [ ] README.md exists at root, follows the structure above, reads like a person wrote it
- [ ] LICENSE exists at root (MIT, with correct copyright holder)
- [ ] CHANGELOG.md exists at root with v0.1 entry
- [ ] `docs/skill-design-patterns.md` and `docs/build-prompt.md` exist for transparency
- [ ] Installation command in README points to `github.com/brubinsztein/strategic-experimentation-coach`
- [ ] No private/internal references that wouldn't make sense to a public reader
- [ ] All prose has been checked against the AI-tells list

## Test prompts

After building, run the skill on at least these three prompts to verify behaviour:

1. **Vague start:** *"We're losing engagement with casual subscribers and I don't know where to start."* — should trigger entry triage, route to Phase 1, push back if the user's first attempt at a theoretical question is solution-shaped.

2. **Question already framed:** *"How can we increase engagement depth among cool subscribers? I want to map out our strategy."* — should skip directly to Phase 2, propose strategic hypotheses from the patterns library.

3. **Tactics already chosen, wants experiments:** *"I want to test whether better content discovery would help retention. Help me design experiments."* — should route to Phase 5, force hypothesis restatement, surface skipped assumptions, propose cheapest-first experiments.

For each, check:
- Pushback fires when it should
- Multiple choice is used where appropriate
- Pattern library options are proposed before the user is asked to generate
- The running doc is written and shown at checkpoints
- The Mermaid diagram renders correctly at Phase 4
- The skill's tone reads like plain prose, not AI-tinged marketing speak

If any test produces a weak or off-pattern response, treat the issue as a skill-improvement signal: update SKILL.md or the relevant reference, then re-test. Don't overfit to the test prompts — the skill needs to generalise.

## After the build

Once the skill folder is complete and tests pass:

1. **Initialise the git repo** at the root of the skill folder.
2. **First commit**: all files as v0.1.
3. **Create the GitHub repo** under `brubinsztein/strategic-experimentation-coach` (you may need to prompt the user to do this via the GitHub web UI, or use `gh repo create` if the GitHub CLI is available).
4. **Push v0.1**.
5. **Suggest to the user**: tag the release as `v0.1.0` so future versions can be tracked cleanly.

Tell the user:
- Where the local repo lives
- What the install command will be once pushed
- A reminder that v0.1 is expected to evolve, so they should treat first PRs from users (issues, edge cases) as valuable signal

## Iteration notes

This is v0.1 of the skill and v0.1 of the public repo. Likely to need refinement:

- Pushback aggressiveness (currently codified as strict — may need to soften based on user feedback)
- Pattern library coverage (currently focused on engagement/retention — will need monetisation and acquisition patterns added)
- Phase 5 pacing (one tactic per session is the current rule — may adjust based on real usage)
- Description fine-tuning (Anthropic's skill-creator has a description-optimisation loop; worth running once the skill has some real usage data)
- README iteration once real users land on the repo

When changes are made, version the relevant doc (`v0.2`, etc.) and note the change in CHANGELOG.md.

---

## If you have the skill-creator skill available

You can invoke `skill-creator` to walk through this build (intent is pre-captured here, so it can move quickly to draft + test) — or build directly. If using skill-creator, hand it this entire prompt as the captured intent and let it drive.

When you're done, present the final repo folder structure and tell me where it was saved.
