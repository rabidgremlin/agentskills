---
name: setup-devcontainer
description: Create or refresh a standard minimal `.devcontainer` setup for Codex-oriented AI experimentation. Use when Codex is asked to add devcontainer support, create `.devcontainer/devcontainer.json`, create `.devcontainer/complete_setup.sh`, set up a container with Python, uv, Node, GitHub CLI, and Codex CLI, or reproduce the Rabidgremlin minimal Codex devcontainer pattern.
---

# Setup Devcontainer

## Workflow

Create or update a target project's `.devcontainer` directory with the bundled templates:

- `assets/devcontainer.json` -> `.devcontainer/devcontainer.json`
- `assets/complete_setup.sh` -> `.devcontainer/complete_setup.sh`

Before writing files, inspect the target project for an existing `.devcontainer` directory. If either target file already exists, preserve it unless the user explicitly asks to overwrite or update it. If updating an existing file, keep unrelated local customization when it is compatible with the standard setup.

## Standard Files

Use the bundled templates as the source of truth. The standard setup uses:

- `mcr.microsoft.com/devcontainers/base:trixie`
- Dev Container features for GitHub CLI, Node, Python, and uv
- `postCreateCommand` set to `bash -i .devcontainer/complete_setup.sh` because `nvm` needs an interactive shell
- `complete_setup.sh` to install latest LTS Node via `nvm` and install `@openai/codex` globally

After creating `complete_setup.sh`, make it executable when the host supports Unix mode bits.

## Verification

Check that both files exist in `.devcontainer`. For `devcontainer.json`, keep the JavaScript-style comment from the template because VS Code devcontainer configuration accepts JSON with comments.

When reporting completion, mention that the user can launch the devcontainer in VS Code and run:

```bash
codex -s danger-full-access --search
```
