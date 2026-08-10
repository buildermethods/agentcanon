# Agent Instructions

This file is the single source of truth for agent instructions in this repo.
`CLAUDE.md` is a symlink to this file. Edit only `AGENTS.md`.

## About this repo

agentcanon is a public offering by Brian Casel / Builder Methods: a
convention that gives users one canonical home for agent skills and
instructions, wired to every tool via symlinks. **The entire product is
`README.md`**: the convention, the copy/paste setup prompt, and the
"going forward" rules. There is no code. The repo practices its own
convention (this file + the committed `CLAUDE.md` symlink), which doubles
as a live demo that git handles symlinks.

## Hard rules

- **README.md is the whole product.** No scripts, manifests, config files,
  or additional docs. If a feature seems to need a new file, it doesn't
  belong in agentcanon.
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
