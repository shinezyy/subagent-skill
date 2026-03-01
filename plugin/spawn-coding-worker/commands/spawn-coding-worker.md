---
description: "Spawn a coding subagent (claude, codex, gemini, or kimi) via spawn-coding-worker.sh"
argument-hint: "--cli claude|codex|gemini|kimi --name <name> --type coder|reviewer|tester --task \"<task>\""
allowed-tools: ["Bash(${CLAUDE_PLUGIN_ROOT}/skills/spawn-coding-worker/scripts/spawn-coding-worker.sh:*)"]
---

# Spawn Coding Worker

Execute the spawn-coding-worker script with the provided arguments:

```!
"${CLAUDE_PLUGIN_ROOT}/skills/spawn-coding-worker/scripts/spawn-coding-worker.sh" $ARGUMENTS
```
