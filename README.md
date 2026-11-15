# mentor-skill

A Claude Code skill that teaches you instead of writing your code.

## Install (1 minute)

```bash
git clone https://github.com/s403o/mentor-skill.git
mkdir -p ~/.claude/skills/mentor
cp mentor-skill/skills/mentor/SKILL.md ~/.claude/skills/mentor/
```

Restart Claude Code. Then type:

```
/mentor learn docker volumes
```

## Commands

| Type this | To do this |
|---|---|
| `/mentor learn <topic>` | Learn a new topic (short, 80/20) |
| `/mentor learn <topic> --deep` | Learn a topic in full detail |
| `/mentor <problem>` | Solve a problem with hints, not answers |
| `/mentor review` | Get questions about the code you wrote |
| `/mentor exit` | End with a 4-line recap |

Two more: `/mentor fast` leaves mentor mode for one urgent problem. `/mentor log` shows your weak areas.

## How learn mode works

1. Claude asks what you already know.
2. It teaches only the core 20% that gives 80% of the results: analogies, one diagram, one real example.
3. It asks 2 or 3 questions to check you really get it.
4. You build one small exercise yourself.
5. Optional: it saves a reference card to `~/.claude/mentor_notes/`.

Want everything, not just the core? Add `--deep`.

## How solve mode works

1. Claude asks what you tried and what you think the error means.
2. It gives hints, smallest first:
   - What do you expect here?
   - Where would you look?
   - Look at this file. What do you see?
   - Here is how it works (no code)
   - A skeleton with `___` blanks you fill in
3. You write the fix. Claude never does.

## What you get over time

After each topic or problem, Claude adds a line to `~/.claude/mentor_log.md`:

```markdown
## 2026-11-15 | Go channels | solve
- Weak: channel close semantics
- Solid: select with default
```

Read it weekly. It shows exactly what to study next.

## Rules Claude follows

- Never writes or edits your project files
- Never gives the full solution, even if you push
- Asks one question at a time
- Asks "why do you think that?" when you guess

---

Built on ideas from [ahmealy/mentor-agent-skill](https://github.com/ahmealy/mentor-agent-skill) and [Sensei](https://github.com/github/awesome-copilot/blob/main/agents/mentoring-juniors.agent.md) (both MIT); extended with learn mode, 80/20 learning, and new teaching principles.

PRs welcome. License: MIT.
