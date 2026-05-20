# Strategic Experimentation Coach

> A Claude skill that helps product managers decompose strategic goals into testable hypotheses, prioritise tactics, and design lightweight experiments, with pushback discipline baked in.

Product teams habitually jump from a goal to a solution and only then ask "how do we test it?" By that point the assumptions baked in are already mostly determined. This skill enforces the missing step: decompose the goal, surface the assumptions, find the cheapest test that could kill the idea. It is built for PMs, product teams, and founders who would rather know they were wrong in a week than ship and find out in a quarter.

## What it does

The skill runs an eight-phase workflow:

- **Phase 0** — Entry triage. Detect where you're starting (vague problem, framed question, chosen tactics, or pure optimisation) and route accordingly.
- **Phase 1** — Frame a theoretical question. Push back on solution-shaped or yes/no questions.
- **Phase 2** — Propose strategic hypotheses. Distinct directions, not rephrasings.
- **Phase 3** — Propose functional hypotheses (tactics) under each strategic hypothesis, then prioritise.
- **Phase 4** — Render the full tree as a Mermaid diagram and checkpoint with the user.
- **Phase 5** — Per-tactic deep-dive: if-then-because hypothesis statement, typed assumption list with LOFAs marked, confidence ratings with evidence cited.
- **Phase 6** — Experiment design. Cheapest test first, with explicit decision criteria and cost-of-failure framing.
- **Phase 7** — Handoff and optional loop to the next priority tactic.

The skill writes a project folder at `./strategic-experiments/<question-slug>/` containing a tree map (`00-map.md`) and per-tactic deep-dives (`01-...`, `02-...`). Each per-tactic doc ends with a sequenced experiment plan that names who would run each test.

A short session looks like this:

```
You: We're losing engagement with casual subscribers and I don't know where to start.

Skill: Activating strategic-experimentation-coach. I'll help you decompose
       this into testable hypotheses and design experiments. This goes in
       phases — push back at any point if something doesn't fit.

       Where are you starting from?
       1. Vague problem or goal, help me frame it
       2. I have a theoretical question or strategy, help me break it down
       3. I have tactics already, help me design experiments
       4. Pure optimisation (A/B on a known thing), skip the framework

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

- _"Help me figure out how to grow engagement among casual users."_
- _"I have a theoretical question I want to break down into experiments."_
- _"How should we test whether better content discovery would help retention?"_

Or invoke it directly:

```
/strategic-experimentation-coach
```

## How it works

`SKILL.md` orchestrates the eight phases and the conversation contract. The two files in `references/` are loaded on demand: `pattern-library.md` for the framework and domain patterns the skill proposes, and `pushback-rules.md` for the reject criteria at each phase. The running docs are plain markdown the user can edit between sessions, so the skill re-reads them at the start of each phase rather than relying on conversation memory.

The skill uses Claude Code's built-in `AskUserQuestion` tool for every choice, confirmation, and rating step, so the conversation moves through structured prompts rather than long prose dumps. The tool caps options at four per question; the skill is written around that constraint.

## Frameworks this synthesises

This skill stands on the shoulders of several established product discovery and growth experimentation frameworks:

- **Marty Cagan / SVPG (INSPIRED)** — the four product risks
- **Teresa Torres (Continuous Discovery Habits)** — opportunity solution trees, assumption mapping
- **David Bland and Alex Osterwalder (Testing Business Ideas)** — the experiment library
- **Itamar Gilad (Evidence Guided / GIST)** — the confidence meter
- **Jonny Longden / Speero (The Apollo Principle, XOS)** — the theoretical-question to strategic-hypothesis to functional-hypothesis hierarchy

See `docs/skill-design-patterns.md` for how these come together and why the skill is monolithic rather than chained sub-skills.

## Contributing

Issues and PRs welcome. The skill is v0.1 and expected to evolve.

To extend the pattern library for a different domain (B2B SaaS, marketplaces, e-commerce), add a section to `references/pattern-library.md` Part 3 with the typical assumption sets for the domain and add domain-specific anti-patterns to Part 5. Send a PR.

## License

MIT. See [LICENSE](LICENSE).

## Credits

Built by [@brubinsztein](https://github.com/brubinsztein). Skill format follows [Anthropic's Agent Skills standard](https://github.com/anthropics/skills). Writing-quality pass uses principles from the [humanizer skill](https://github.com/blader/humanizer).
