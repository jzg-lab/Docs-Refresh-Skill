# Install `docs-refresh` in Codex

This repository publishes a reusable skill folder, not a Codex plugin.

Install the `docs-refresh/` directory into your local Codex skills directory so Codex can auto-discover it.

## Install

```bash
git clone https://github.com/jzg-lab/Docs-Refresh-Skill.git
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R Docs-Refresh-Skill/docs-refresh "${CODEX_HOME:-$HOME/.codex}/skills/"
```

If `docs-refresh` is already installed, replace the existing folder with the newer copy from this repository.

## Update

Pull the latest repository changes and copy `docs-refresh/` into the same local skills directory again.

## Verify

Start a new Codex session in a repository and ask Codex to refresh the repository's authoritative docs.

Codex should discover the `docs-refresh` skill and use the routed workflow from `docs-refresh/SKILL.md`.
