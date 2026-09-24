---
name: bench-loop
description: >-
  Use for Vorxeo WIP=1 bench loops. Run bench → read real % from output (never
  invent metrics) → find weakness in ORIGINAL motor/evidence (not
  scorer/adapter) → improve → re-run before next bench. Queue example
  DEMM/Authority Record → Auditable Agents → AgentDojo. Measurement ≠
  certification. Overclaim 0% is good when applicable.
---
# Bench Loop

Vorxeo WIP=1 bench discipline: one improvement in flight; measure honestly; fix the motor, not the scoreboard.

## When this skill applies

- Running or interpreting product benches (governance / authority / agent audit suites).
- Choosing the next WIP item from the bench queue.
- After a model or policy change that claims "better on X bench".
- Anytime someone pastes a percentage without a result file — refuse and re-measure (`verified-delivery`).

## WIP=1 loop

```text
1. Run bench → redirect full output to a result file
2. Read real metrics from that file (never invent %)
3. Find weakness in ORIGINAL motor / evidence path
4. Improve that motor (one coherent change)
5. Re-run the SAME bench before starting another bench or another WIP
6. Only then move queue pointer
```

**Failure mode multi-WIP**: three "improvements" without a re-run → metrics fiction.

**Failure mode scorer-gaming**: change adapter/scorer/prompt wrapper to raise % while motor behaviour unchanged — forbidden. Fix evidence generation, policy motor, retrieval, or authority record path.

## Read real metrics

Rules:

- Percentage, pass counts, and per-task outcomes come from the bench output file only.
- If the run crashed or truncated, Status = Failed / Incomplete — not "about 70%".
- Overclaim: stating a higher % than the file → treat claim as invalid; prefer recording **Overclaim 0%** until a clean Verified run exists.
- **Overclaim 0% is good** when applicable: honest zero beats fake sixty.

Quote the line you used, e.g. `Overall: 42.0% (21/50)` from `/tmp/bench-demm.txt`.

## Motor vs scorer

| Fix here (allowed) | Not here (disallowed as "improvement") |
|--------------------|----------------------------------------|
| Authority record generation | Softening the scorer |
| Policy / gate motor | Filtering hard tasks out of the suite |
| Evidence completeness | Golden-answer leakage into input |
| Tool-use correctness | Custom adapter that maps failures to pass |

If the only change is in harness/scorer/adapter, label the PR **harness**, not **capability**, and do not advance the product queue on that alone.

## Example queue (Vorxeo)

Default ordering unless product lead overrides:

1. **DEMM / Authority Record**
2. **Auditable Agents**
3. **AgentDojo**

Rules:

- Finish WIP on current bench (Verified re-run) before starting the next name in the queue.
- Do not cherry-pick AgentDojo wins while Authority Record is red unless explicitly re-prioritized in the handoff packet.
- Document queue position in the delivery receipt.

## Measurement ≠ certification

| Measurement | Certification |
|-------------|---------------|
| Bench % on suite S at commit C | Claim that product is safe/compliant for production governance |
| Useful for regression and iteration | Requires gates, adversarial-qa, fail-closed-review, migrations, contracts |

**Failure mode bench-as-cert**: "82% on DEMM ⇒ ship authz" — false. Bench guides WIP; `fail-closed-review` + `adversarial-qa` + Verified deny paths certify controls.

State explicitly in reports: `Measurement only; not a compliance certification.`

## Procedure checklist

- [ ] Result file path recorded
- [ ] Metrics copied verbatim from file
- [ ] Weakness named in motor/evidence (file/symbol)
- [ ] Single WIP change linked
- [ ] Same bench re-run; new result file
- [ ] Delta stated with before/after cites
- [ ] Queue position unchanged until loop closes
- [ ] No certification language

## Delivery snippet

```text
### Bench loop receipt
- Bench: <name>
- Queue position: <n> (<name>)
- Before file: <path> → <verbatim metric>
- Weakness (motor): <path/symbol + one sentence>
- Change: <PR/commit or summary>
- After file: <path> → <verbatim metric>
- WIP status: closed | still-open
- Certification claim: none
```

## Failure modes (named)

| Name | Meaning |
|------|---------|
| **invented-metric** | % not in result file |
| **overclaim** | Stated % > file % |
| **scorer-gaming** | Harness raised score, motor same |
| **multi-WIP** | Multiple changes without re-run |
| **queue-jump** | Next bench started mid-WIP |
| **bench-as-cert** | Measurement sold as certification |
| **stale-baseline** | Compare to memory, not before file |

## Interaction with other skills

- **verified-delivery**: bench output is the result file; same redirect+Read rules.
- **karpathy-method**: measure after change; this skill is the bench-shaped instance of step 6.
- **code-that-holds**: improve holding behaviour in the motor.
- **handoff-faber-rigor**: Faber includes before/after bench receipts; Rigor rejects invented metrics.
- **adversarial-qa**: orthogonal — gates can fail adversarial QA at high bench %; do both.
- **fail-closed-review**: bench green does not Approve an authz PR.

## Anti-patterns

- Averaging three runs and reporting the max.
- Quietly dropping failing tasks from the suite.
- Claiming "overclaim 0%" while still publishing a marketing number elsewhere — one number, Verified.
- Starting Auditable Agents because DEMM "feels stuck" without a written re-prioritization.
