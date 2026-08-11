# Agent Instructions

This file is the single source of truth for agent instructions in this repo.
`CLAUDE.md` is a symlink to this file. Edit only `AGENTS.md`.

## About this repo

agentcanon is a public offering by Brian Casel / Builder Methods: a
convention that gives users one canonical home for agent skills and
instructions, wired to every tool via symlinks. **The product is
`README.md`**: the convention, the copy/paste setup prompt, and the
"going forward" rules. Two optional extras live in `.agents/skills/`:
the `agentcanon-manifest` skill (a SKILL.md plus a bundled
`skills-manifest.html` template that agents copy to `~/.agents/` and fill
with skill data) and the `agentcanon-repo` skill (a single SKILL.md that
converts any repo to the convention via an inspect → plan → approval →
execute flow). The repo practices its own convention (the committed
`CLAUDE.md` and `.claude/skills` symlinks), which doubles as a live demo
that git handles symlinks.

## Hard rules

- **README.md plus the two optional skills are the whole product.**
  No other scripts, config files, or docs. If a feature seems to need a
  new file, it doesn't belong in agentcanon.
- **The skills stay strictly optional and self-contained.** The core
  convention never depends on either. `skills-manifest.html` is one file
  with no external requests; all data lives in its embedded
  `manifest-data` JSON block, written by agents following the skill's
  SKILL.md, and the page renders sensibly when that block is empty.
  `agentcanon-repo` is one SKILL.md whose target state and commands must
  match the README's setup prompt, and it never moves, merges, or
  deletes anything before the user approves its plan.
- **The embedded setup prompt must stay self-contained.** It has to work
  pasted into any agent with nothing fetched: the exact target layout, the
  exact symlink commands (including the relative `../.agents/skills` form),
  and the inspect → plan → approval protocol before anything of the user's
  is moved, merged, or deleted.
- Simplicity and light weight are the value proposition. When editing the
  README, cut before adding, and keep the prompt block and the convention
  diagram in agreement.

## Testing

Nothing to run. Review = re-read README.md as a first-time user, and check
that the prompt block's layout and commands match the convention diagram.
