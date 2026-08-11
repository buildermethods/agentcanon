# agentcanon

**One canonical home for all your agent skills and instructions.**

Most AI tools have settled on a standard: skills live in `.agents/skills/`
and instructions live in `AGENTS.md`. Codex, Cursor, and most newer tools
read them natively. But a few holdouts (_ahem, Claude Code_) still look in
their own locations instead, so you end up with duplicate skill folders, a
`CLAUDE.md` here and an `AGENTS.md` there, copies that drift apart, and no
idea which one is real.

[agentcanon](https://github.com/buildermethods/agentcanon) is the simplest
possible fix: everything lives in the standard locations, and symlinks
point the holdouts at them.

Point your agent at this repo to get set up.

- [The convention](#the-convention)
- [Setup](#setup)
- [Going forward](#going-forward)
- [Sync across machines](#sync-across-machines-optional)
- [Skills manifest](#skills-manifest-optional)

## The convention

Everything real lives in the open-standard `.agents` locations. Everything
else is a symlink, so that you don't need duplicates.

```
~/.agents/skills/             ← your global skills, the ONE real copy
~/.claude/skills              → symlink to ~/.agents/skills

any-project/
  AGENTS.md                   ← the real agent instructions
  CLAUDE.md                   → symlink to AGENTS.md
  .agents/skills/             ← the project's real skills
  .claude/skills              → symlink to .agents/skills
```

Why `.agents` and `AGENTS.md` as canon? They're the vendor-neutral
[Agent Skills](https://agentskills.io) / AGENTS.md standards that Codex,
Cursor, and a growing list of tools already read natively. Claude Code
reads its own `.claude` locations, hence the two symlinks. If a tool needs
its own pointer someday, that's one more symlink, never a copy.

(This repo practices the convention: its `CLAUDE.md` and `.claude/skills`
are committed symlinks.)

## Setup

Paste either prompt to your agent (Claude Code, Codex, or any agent
running on your machine).

**The one-liner**, if your agent can fetch URLs:

```
Read https://github.com/buildermethods/agentcanon and set up the
agentcanon convention on this machine and in the current repo (if we're
in one).
```

**The full prompt**, self-contained with nothing to fetch:

```
Set up the agentcanon convention on this machine (and in the current repo,
if we're in one): one canonical home for agent skills and instructions,
with every tool wired to it by symlinks.

Target state, global:
  ~/.agents/skills/    the one real home for global skills
  ~/.claude/skills     symlink -> ~/.agents/skills

Target state, per project repo:
  AGENTS.md            the real agent instructions
  CLAUDE.md            symlink -> AGENTS.md
  .agents/skills/      the repo's real skills
  .claude/skills       symlink -> ../.agents/skills

Ground rules:
1. Inspect first. Check the locations above, plus any other agent skill
   directories or instruction files on this machine, and report what you
   find: what's already wired, what's a real file or directory sitting
   where a symlink belongs, duplicates, same-name skills that differ.
2. If a directory or symlink from the target state is missing and
   nothing sits in its place, create it, using exactly these forms:
     mkdir -p ~/.agents/skills
     ln -s ../.agents/skills ~/.claude/skills
     ln -s AGENTS.md CLAUDE.md                            (in a repo)
     mkdir -p .agents/skills
     ln -s ../.agents/skills .claude/skills               (in a repo)
   If a repo has no AGENTS.md yet, create a minimal starter before
   linking to it.
3. Anything else (moving, merging, or deleting my files) happens only
   through a plan you show me and I approve. Identical duplicates: keep
   the canon copy. Same-name skills that differ: one line each on how
   they differ, plus your recommendation. A CLAUDE.md and AGENTS.md that
   both have content: propose the merged file.
4. Finish by verifying every symlink resolves and showing a short
   pass/fail report of the final state.

If my setup doesn't match these assumptions, adapt and explain your
reasoning rather than forcing the pattern.
```

Run it once per machine; the project part runs once per repo. It's also
your once-and-for-all cleanup: skills scattered across months of installs
all end up in one place you trust, with your approval at every step.

## Going forward

Going forward, stick to the agentcanon convention by following these best practices:

1. **Installing skills.** A skill is a folder with a `SKILL.md` inside. When it's a skill you want to use globally, place it in `~/.agents/skills/`. When it's a project-specific skill, place it in your repo's `.agents/skills/`.  Same location applies for custom skills you create. Claude Code (and any other tool you've symlinked) will see your agent skills normally. 
2. **Never put skill folders in a `.claude/skills/` path.** Same goes for other skills folders. Those should be symlinked to `~/.agents/skills/` or `<project>/.agents/skills/`.
3. Write agent instructions to your project's `AGENTS.md`. `CLAUDE.md` should be symlinked to it.
4. Use a template repo? Build these conventions into it (using the prompt above) so that you're always using the agentcanon convention.

## Sync across machines (optional)

Git handles syncing; no sync service needed.

- **Global skills:** make `~/.agents/` a git repo and push it to a private
  remote. Clone it on your other machines; syncing is a push and a pull.
- **Projects:** commit your repo's `.agents/` folder and symlinks normally.
  They travel with the project like any other code.

## Skills manifest (optional)

A nicety, not part of the convention; skip it freely. The manifest is a
single dependency-free HTML page at `~/.agents/skills-manifest.html` that
lists every skill on your machine (name, description, location, created
date), sortable and filterable by global or project, plus a list of your
skills folder symlinks. Open it in any browser.

If you want it, tell your agent:

```
Install the agentcanon-manifest skill from
https://github.com/buildermethods/agentcanon: copy
.agents/skills/agentcanon-manifest/ into ~/.agents/skills/, then use it
to install the skills manifest.
```

Refresh it anytime with "update the skills manifest".

---

Created by Brian Casel from [Builder Methods](https://buildermethods.com).

Subscribe to Brian on [YouTube](https://youtube.com/@briancasel) or
[the newsletter for AI builders](https://buildermethods.com).
