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


## Licensing

- Code: [Apache-2.0](LICENSE)
- Docs, paper, figures: CC BY 4.0

