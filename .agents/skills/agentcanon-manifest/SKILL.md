---
name: agentcanon-manifest
description: Install or update the skills manifest, a standalone HTML page at ~/.agents/skills-manifest.html that lists every skill on this machine. Use when asked to install, update, refresh, or rebuild the skills manifest.
---

# Skills manifest

The manifest is one self-contained HTML file at `~/.agents/skills-manifest.html`.
All of its data lives in the embedded JSON block:
`<script type="application/json" id="manifest-data">`. Change nothing in the
file except that block. This skill only reads skill folders; never modify them.

## Install

Copy `skills-manifest.html` (it sits next to this SKILL.md) to
`~/.agents/skills-manifest.html`, then follow Update. Overwriting an existing
manifest is fine; it contains nothing hand-written.

## Update

1. Collect skill folders. A skill is any directory containing a `SKILL.md`.
   - Global: each directory in `~/.agents/skills/`.
   - Project: search the user's system for every project folder holding
     skills. Crawl likely code locations under the home directory for
     `.agents/skills/` directories, and for real (non-symlink)
     `.claude/skills/` directories, that contain skills. Skip
     `node_modules`, dependency caches, and other vendored or system
     paths. List the skills of every project found.
2. Build one record per skill:
   - `name`: the folder name.
   - `description`: the first sentence of the `description` field in its
     SKILL.md frontmatter, or of the first body paragraph if no frontmatter.
   - `location`: absolute folder path, with the home directory written as `~`.
   - `scope`: `"global"` or `"project"`.
   - `created`: the folder's creation (birth) time if the OS provides it,
     else its modification time, as `YYYY-MM-DDTHH:MM`.
3. Collect skills folder symlinks: `~/.claude/skills`, each scanned project's
   `.claude/skills`, and any other tool symlink into a `.agents/skills`
   location you find. One record each:
   - `path`: the symlink, `target`: what it points to, `ok`: true when it
     resolves to the matching `.agents/skills` folder.
4. Replace the JSON inside the `manifest-data` block with:

   ```json
   {"generated": "YYYY-MM-DDTHH:MM", "skills": [...], "symlinks": [...]}
   ```

5. Identify potential duplicates: the same skill name in more than one
   location. The page badges these automatically; you should also compare
   each set of copies so you can say whether they're identical (one is
   safe to remove) or differ.
6. Report the skill and symlink counts, each potential duplicate with its
   locations and identical-or-differs status, and that the page is at
   `~/.agents/skills-manifest.html`. Don't remove or change duplicates;
   just inform the user.
