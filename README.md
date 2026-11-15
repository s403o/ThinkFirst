# mentor-skill

A Claude Code skill that makes the AI teach you instead of doing the work for you.

You write the code. Claude teaches new topics with a mental model first, asks questions, gives hints that escalate step by step, reviews what you wrote, and keeps a log of your weak areas.

## Why

Using AI as an answer machine is fast, but you stop building the skill yourself. This skill is a drill: you stay in charge of the thinking, and the AI acts as a mentor.

## Install

```bash
git clone https://github.com/s403o/mentor-skill.git
mkdir -p ~/.claude/skills/mentor
cp mentor-skill/skills/mentor/SKILL.md ~/.claude/skills/mentor/SKILL.md
```

Restart Claude Code. The skill only runs when you type `/mentor`.

## Usage

| Command | What it does |
|---|---|
| `/mentor <topic>` | Solve a problem with Socratic hints |
| `/mentor learn <topic>` | Learn a new topic; 80/20 by default |
| `/mentor learn <topic> --deep` | Learn a topic in full detail |
| `/mentor review` | Review the code you just wrote |
| `/mentor fast` | Urgent work; leave mentor mode for this problem |
| `/mentor log` | Show your weak areas |
| `/mentor exit` | End the session with a short recap |

Examples:

```
/mentor learn kubernetes services
/mentor learn go concurrency --deep
/mentor my goroutines hang when the channel is closed
```

## Two modes

### Learn mode: understand first

For a topic you don't know yet. Mental model before code.

**80/20 (default).** Based on the Pareto principle: about 20% of the concepts give about 80% of the results. Claude teaches only that core:

1. The problem the topic solves, with one analogy
2. The 3 to 5 vital concepts: what, why, when
3. One ASCII diagram of how they fit together
4. How it links to what you already know
5. A "skip for now" list of what was left out on purpose

**Deep (`--deep`).** All building blocks, the full lifecycle, a real-world scenario, comparisons, edge cases, and pitfalls.

Both are Socratic around the teaching:

- **Before:** Claude asks what you think the topic solves, and starts from your answer.
- **After:** no "do you understand?". You get 2 or 3 questions that only someone who understands can answer. A wrong answer gets a follow-up question before any correction.
- **Then:** one small exercise you build yourself, in solve mode.
- **Finally:** an optional reference card saved to `~/.claude/mentor_notes/<topic>.md`.

### Solve mode: think it through

For a problem you are working on.

**Context first.** Before any hint, Claude asks what you are trying to do, what you tried, and what you think the error means.

**Hint tiers.** Claude starts at Tier 1 and only moves up when you are stuck. Ask for a bigger hint and it jumps one tier.

| Tier | What it does |
|---|---|
| 1. Conceptual | Asks what you expect and why |
| 2. Directional | Points to where to look |
| 3. Structural | Points to a specific file or function |
| 4. Mechanism | Explains how it works, in plain language |
| 5. Scaffold | Pseudocode or a skeleton with `___` blanks; you fill them |

If the problem shows a missing foundation, Claude offers `/mentor learn` for that concept first.

**Guess check.** If you guess, Claude asks for your reasoning before confirming.

**Syntax exception.** Ask for syntax only and you get a generic example of max 3 lines, never your solution.

## Review

When your code works, Claude asks questions on correctness, security, performance, and readability. It does not fix anything.

## Fast mode

For production issues or deadlines, `/mentor fast` leaves mentor mode for one problem. The topic is logged as `Debt` so you can come back to it.

## Weak area log

After each problem or topic, Claude appends to `~/.claude/mentor_log.md`:

```markdown
## 2026-11-15 | Go channels | solve
- Weak: channel close semantics (Tier 3+)
- Solid: select with default (self-solved)
```

Over time this file shows where your understanding is thin.

## What it will never do

- Write or edit files in your project
- Give a complete solution, even as an "example"
- Give in to "just tell me"; it offers the next hint tier instead
- Skip the understanding check in learn mode

## Credits

This skill merges ideas from:

- [ahmealy/mentor-agent-skill](https://github.com/ahmealy/mentor-agent-skill) (MIT): base structure, hint tiers, guess check, weak area log
- [Sensei - Junior Mentor](https://github.com/github/awesome-copilot/blob/main/agents/mentoring-juniors.agent.md) from [github/awesome-copilot](https://github.com/github/awesome-copilot) (MIT) by Thomas Chmara and François Descamps: context gathering, scaffold hints, review axes, urgency mode, session recap
- A community "mental model first" learning methodology: teaching principles and the structure of learn mode
- The 80/20 (Pareto) learning rule: the default depth of learn mode

## Contributing

Issues and PRs are welcome, especially better hint wording and real session examples.

## License

MIT
