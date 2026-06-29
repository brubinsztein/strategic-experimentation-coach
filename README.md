# Strategic Experimentation Coach

> A Claude skill that helps product managers decompose strategic goals into testable problem and solution hypotheses, prioritise solutions, and design a minimum viable test (MVT) that validates or kills each bet, with pushback discipline baked in.

Product teams habitually jump from a goal to a solution and only then ask "how do we test it?" By that point the assumptions baked in are already mostly determined. This skill enforces the missing step: decompose the goal, surface the assumptions, find the lowest-effort test that could kill the idea. It is built for PMs, product teams, and founders who would rather know they were wrong in a week than ship and find out in a quarter.

## What it does

The skill runs a phased workflow down a six-level spine (Theoretical question → Strategic hypothesis → Problem hypothesis → Solution hypothesis → MVT → validated/production solution), with a confidence gate at each step:

- **Phase 0**: Entry triage. Detect where you're starting (vague portfolio goal, a direction, a problem, a solution, or pure optimisation) and route entry at any altitude.
- **Phase 0.5**: Discovery and context. Probe for the product, cohort definition, metric and baseline, prior attempts, constraints, and test capability before any problem work, and offer to save reusable context to `product-context.md`.
- **Phase 1**: Frame a theoretical question (portfolio altitude). Push back on solution-shaped or yes/no questions.
- **Phase 2**: Propose strategic hypotheses (portfolio altitude). Distinct directions, not rephrasings.
- **Phase 3**: Elicit problem hypotheses: broken, observable behaviours for the cohort, grounded in data.
- **Phase 4**: Propose 2 to 3 solution hypotheses per problem, group those sharing a LOFA, and prioritise.
- **Phase 5**: Render the full tree as a Mermaid diagram and checkpoint with the user.
- **Phase 6**: Per-solution deep-dive: full-format statement (causal chain, guardrail), separate belief and LOFA lists, inline confidence.
- **Phase 7**: MVT design. Lowest-effort test that validates or kills the bet, with leading/lagging/guardrail metric tiers and decision criteria.
- **Phase 8**: Handoff and optional loop to the next priority solution.

The skill writes a project folder at `./strategic-experiments/<question-slug>/` containing a tree map (`00-map.md`) and per-solution deep-dives (`01-...`, `02-...`). Each per-solution doc ends with a prioritised MVT plan that names who would run each test.

A short session looks like this:

```
You: We're losing engagement with light-engagement subscribers and I don't know where to start.

Skill: Activating strategic-experimentation-coach. I'll help you decompose
       this into problem and solution hypotheses and design a minimum viable
       test. This goes in phases; push back at any point if something doesn't fit.

       Where are you starting from?
       1. I have a vague portfolio goal, help me frame it
       2. I have a direction or strategy, help me break it down
       3. I have a project or problem in hand
       4. I have a solution already, help me state and test it
       5. Pure optimisation (A/B on a known thing)

You: 1

Skill: What's the question you're trying to answer? One sentence, in your
       own words.
```

## Installation

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/brubinsztein/strategic-experimentation-coach.git ~/.claude/skills/strategic-experimentation-coach
```

The skill becomes available the next time you start Claude Code in a project.

### Claude.ai

Claude.ai supports custom skills via the skill upload UI. Zip the repo contents (or upload the folder) following [Anthropic's skill upload docs](https://github.com/anthropics/skills).

## Usage

Once installed, the skill triggers automatically when you ask Claude things like:

- _"Help me figure out how to grow engagement among light-engagement users."_
- _"I have a theoretical question I want to break down into experiments."_
- _"How should we test whether better content discovery would help retention?"_

Or invoke it directly:

```
/strategic-experimentation-coach
```

## How it works

`SKILL.md` orchestrates the phases and the conversation contract. The two files in `references/` are loaded on demand: `pattern-library.md` for the framework and domain patterns the skill proposes, and `pushback-rules.md` for the reject criteria at each phase. The running docs are plain markdown the user can edit between sessions, so the skill re-reads them at the start of each phase rather than relying on conversation memory.

Context that holds across projects (the product, business model, cohorts, metrics, and terminology) is saved once to `./strategic-experiments/product-context.md` and read at the start of every project, so you do not repeat it each session. Project-specific framing stays in that project's `00-map.md`.

The skill uses Claude Code's built-in `AskUserQuestion` tool for every choice, confirmation, and rating step, so the conversation moves through structured prompts rather than long prose dumps. The tool caps options at four per question; the skill is written around that constraint.

## Viewing the docs

The running docs use Mermaid diagrams for the tree. To see them rendered rather than as raw code:

- **VS Code**: install a Mermaid preview extension (for example "Markdown Preview Mermaid Support"), then open any doc and use preview mode with `Cmd+Shift+V` (macOS) or `Ctrl+Shift+V` (Windows/Linux). The diagram and the formatted markdown render side by side with the source.
- **GitHub** and most markdown viewers render Mermaid natively, so the diagrams show without any extension.

If a diagram shows as a `mermaid` code block instead of a picture, the viewer lacks Mermaid support; install the extension above.

## Frameworks this synthesises

This skill stands on the shoulders of several established product discovery and growth experimentation frameworks:

- **Marty Cagan / SVPG (INSPIRED)**: the four product risks
- **Teresa Torres (Continuous Discovery Habits)**: opportunity solution trees, assumption mapping
- **David Bland and Alex Osterwalder (Testing Business Ideas)**: the experiment library
- **Itamar Gilad (Evidence Guided / GIST)**: the confidence meter
- **Jonny Longden / Speero (The Apollo Principle, XOS)**: horse-race iterative learning, tests inform decisions but aren't decisions
- **Applied product operating model**: the six-level spine, the confidence gate at each step, and the MVT "validate or kill" framing

See `docs/skill-design-patterns.md` for how these come together and why the skill is monolithic rather than chained sub-skills.

## Contributing

Issues and PRs welcome. The skill is v1.0 and expected to evolve.

To extend the pattern library for a different domain (B2B SaaS, marketplaces, e-commerce), add a section to `references/pattern-library.md` Part 3 with the typical assumption sets for the domain and add domain-specific anti-patterns to Part 5. Send a PR.

## License

MIT. See [LICENSE](LICENSE).

## Credits

Built by [@brubinsztein](https://github.com/brubinsztein). Skill format follows [Anthropic's Agent Skills standard](https://github.com/anthropics/skills). Writing-quality pass uses principles from the [humanizer skill](https://github.com/blader/humanizer).
