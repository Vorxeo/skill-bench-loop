# Bench Loop

Claude Code skill: `bench-loop`

## What

Vorxeo WIP=1 bench discipline: run bench → read real metrics from the output file (never invent %) → fix weakness in the **original motor/evidence**, not the scorer → re-run before next WIP. Measurement ≠ certification. **Overclaim 0%** is good when applicable.

## When to use

Running or interpreting product benches; choosing next WIP from the queue; anyone pastes a % without a result file.

## Install

Copy this folder into your Claude Code skills directory:

```bash
mkdir -p ~/.claude/skills/bench-loop
cp SKILL.md ~/.claude/skills/bench-loop/
```

Claude Code loads `SKILL.md` from `~/.claude/skills/<name>/`.

## Sibling skills

`verified-delivery`, `karpathy-method`, `code-that-holds`, `handoff-faber-rigor`, `adversarial-qa`, `fail-closed-review`

Proposed repos: see [Vorxeo](https://github.com/Vorxeo) `skill-*` packs.

## License

MIT — Copyright (c) 2026 Vorxeo. See [LICENSE](./LICENSE).
