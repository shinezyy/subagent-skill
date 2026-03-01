# spawn-coding-worker Plugin

Claude Code plugin package that embeds one mixed-subagent skill.

## Included components

- `.claude-plugin/plugin.json`
- `commands/spawn-coding-worker.md` → slash command entry point
- `skills/spawn-coding-worker/SKILL.md`
- `skills/spawn-coding-worker/scripts/spawn-coding-worker.sh`
- `skills/spawn-coding-worker/scripts/cc_env.sh`
- `skills/spawn-coding-worker/references/spawn-workflow.md`

`commands/` and `skills/spawn-coding-worker/*` are symlinks to the shared source at:

- `../../skills/spawn-coding-worker/`

Refresh all links after editing shared source:

```bash
./scripts/sync-shared-assets.sh
```

## Purpose

Enable Claude Code main sessions to orchestrate Claude, Codex, Gemini, or Kimi sub-agents through one entrypoint:

- `/spawn-coding-worker:spawn-coding-worker`

Use `--cli` to select runtime (`claude`, `codex`, `gemini`, or `kimi`).

## Installation (Claude Code plugin system)

`claude plugin install` does not support local paths. Copy manually using `cp -rL` or `rsync -aL` to dereference symlinks:

```bash
PLUGIN_CACHE=~/.claude/plugins/cache/local/spawn-coding-worker/0.2.0
rm -rf "$PLUGIN_CACHE"
mkdir -p "$PLUGIN_CACHE"
rsync -aL --delete /path/to/subagent-skill/plugin/spawn-coding-worker/ "$PLUGIN_CACHE/"
```

Then add to `~/.claude/plugins/installed_plugins.json` and restart Claude Code.

> **Important:** Use `rsync -aL --delete`, not plain `cp -r` (copies broken symlinks) or `cp -rL` (fails with "same file" errors when run from repo root).

## Verified Smoke Commands

Run from repository root after skill/plugin is loaded.

```bash
./scripts/spawn-coding-worker.sh --cli codex --name smoke-codex-joke --type coder --task "Tell a joke."
./scripts/spawn-coding-worker.sh --cli gemini --name smoke-gemini-joke --type coder --task "Tell a joke."
./scripts/spawn-coding-worker.sh --cli kimi --name smoke-kimi-explain --type reviewer --task "Explain what this code does: $(cat main.py)"
env -u CLAUDECODE ./scripts/spawn-coding-worker.sh --cli claude --name smoke-claude-joke --type coder --task "Tell a joke."
```

> **Note**: The `env -u CLAUDECODE` prefix is required when spawning Claude workers from within a Claude Code session. This prevents nested session conflicts.
