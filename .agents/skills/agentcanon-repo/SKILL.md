---
name: agentcanon-repo
description: Convert the current repo to the agentcanon convention. Moves skills from non-canonical folders (like a real .claude/skills) into .agents/skills/, replaces those folders with symlinks, merges CLAUDE.md into AGENTS.md, and symlinks CLAUDE.md to it. Use when asked to set up, convert, or migrate a repo to agentcanon.
---

# Convert a repo to the agentcanon convention

Run from the root of the repo to convert. Target state:

```
AGENTS.md            the real agent instructions
CLAUDE.md            symlink -> AGENTS.md
.agents/skills/      the repo's real skills
.claude/skills       symlink -> ../.agents/skills
```

Nothing is moved, merged, or deleted until the user approves the plan in
step 2. Step 1 is read-only.

## 1. Inspect

- Find every skill folder in the repo: a skill is a directory containing
  a `SKILL.md`. Note which live outside `.agents/skills/` — a real
  `.claude/skills/`, or any other tool's skills directory. Skip
  `node_modules` and other vendored or dependency paths.
- Check `AGENTS.md` and `CLAUDE.md`: which exist, which are symlinks,
  and whether both are real files with content.
- Check whether `.claude/skills` (and any other tool skills path found)
  is already a symlink and where it points.
- For each skill that would move, check for a same-name skill already in
  `.agents/skills/` and compare them: identical, or different.

## 2. Plan and get approval

Present one plan listing, specifically:

- Each skill folder that will move, `from -> to`.
- Each folder that will become a symlink, with its exact target (e.g.
  `.claude/skills -> ../.agents/skills`).
- Name collisions: identical copies get one line ("identical; keeping
  the `.agents/skills` copy"); differing copies get one line on how they
  differ plus a recommendation.
- The instructions files: if both `CLAUDE.md` and `AGENTS.md` have
  content, show the proposed merged `AGENTS.md`; if only `CLAUDE.md`
  exists, say it becomes `AGENTS.md`; either way `CLAUDE.md` ends as a
  symlink.
- Anything that will be created from nothing (e.g. a minimal starter
  `AGENTS.md` when neither file exists).

Ask for confirmation and wait. Do not proceed without it. If the user
adjusts the plan, re-present the changed parts.

## 3. Execute

Only after approval, and only what the approved plan says. The usual
commands (use `git mv` for tracked files):

```
mkdir -p .agents/skills
mv .claude/skills/<skill> .agents/skills/<skill>   # per skill
rmdir .claude/skills                                # once emptied
ln -s ../.agents/skills .claude/skills
mv CLAUDE.md AGENTS.md                              # if AGENTS.md didn't exist
ln -s AGENTS.md CLAUDE.md
```

When merging two instruction files, write the approved merged content to
`AGENTS.md`, then remove `CLAUDE.md` and create the symlink.

## 4. Verify

Confirm every symlink resolves to its intended target and each moved
skill's `SKILL.md` is present in `.agents/skills/`. Finish with a short
pass/fail report of the final state.

If the repo doesn't match these assumptions, adapt and explain rather
than forcing the pattern.
