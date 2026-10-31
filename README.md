# Leviathan

**Goal-based evaluation of AI agents on validated CVE environments.**
DSU Undergraduate Student Mentored Research Initiative (SRI).
Muhammad Essa & Oluwajuwon Adedowole · Mentor: Pat Engebretson

Leviathan measures how well frontier and local LLM agents (GPT-5.6 Sol, Claude Opus, Qwen) achieve frozen,
impact-specific goals against independently validated targets for recent CVEs that have no public PoC.

## Architecture

```
            ┌────────────┐   bounded MCP tools    ┌──────────────┐
            │  builder   │ ─────────────────────▶ │   targets    │  (isolated: container / VM / emulator,
            └────────────┘                        │ vuln + patch │   no internet route, snapshot+reset)
                                                  └──────▲───────┘
            ┌────────────┐   attacker-facing tools       │
 task ────▶ │  attacker  │ ──────────────────────────────┘
 packet     │ (model X)  │
            └─────┬──────┘
                  │ claims / artifacts
            ┌─────▼──────┐  hidden flags, manifests, grading logic
            │ evaluator  │  (never visible to builder or attacker)
            └────────────┘
```

Invariants:
1. Builders never attack their own targets.
2. Attackers never see evaluator secrets, flags, or verifier code.
3. A goal contract is frozen before exploitation begins.
4. A result counts only if it **succeeds on the vulnerable target and fails on the patched/negative control**.

## Layout

| Path | Purpose |
|---|---|
| `builder/` | MCP server + tools for assembling approved targets |
| `attacker/` | Shared attacker harness and MCP tools (identical for all models) |
| `evaluator/` | Verifier, flag generation, contract freezing (keep secrets out of git) |
| `targets/` | Target definitions (Dockerfiles, VM/emulation configs). No exploit code |
| `manifests/` | Candidate lists, eligibility records, target manifests |
| `schemas/` | JSON schemas for goal contracts and target manifests |
| `results/` | Run logs and analysis (raw attacker transcripts stay out of the public repo) |
| `docs/` | Timeline, eligibility criteria, methodology |

## Licensing

- Code: [Apache-2.0](LICENSE)
- Docs, paper, figures: CC BY 4.0
- Exploit artifacts and attacker transcripts: **not** covered by the open license. Released only redacted or access-gated (see [RESPONSIBLE_USE.md](RESPONSIBLE_USE.md)).

See [docs/TIMELINE.md](docs/TIMELINE.md) for the schedule.
