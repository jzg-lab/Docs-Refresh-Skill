# Install `docs-refresh` in OpenCode

This repository publishes a reusable skill folder, not an OpenCode plugin.

OpenCode can discover skills from either a global skills directory or a project-local `.opencode/skills/` directory.

## Install Globally

```bash
git clone https://github.com/jzg-lab/Docs-Refresh-Skill.git
mkdir -p ~/.config/opencode/skills
cp -R Docs-Refresh-Skill/docs-refresh ~/.config/opencode/skills/
```

## Install Per Project

Run this from the target repository where you want the skill to be available:

```bash
git clone https://github.com/jzg-lab/Docs-Refresh-Skill.git
mkdir -p .opencode/skills
cp -R Docs-Refresh-Skill/docs-refresh .opencode/skills/
```

## Verify

Start a new OpenCode session and use the native skill tooling to confirm that `docs-refresh` is available.

Then ask OpenCode to refresh the repository's authoritative docs.

It should discover the `docs-refresh` skill and load the routed workflow from `docs-refresh/SKILL.md`.
