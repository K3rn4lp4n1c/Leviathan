# Responsible Use and Release Policy

Leviathan studies AI-generated exploit artifacts for disclosed CVEs. That work is dual-use. This policy
governs what goes into this repository and what is released.

## Never commit
- Working exploit code, payloads, or model-generated attack artifacts
- Full attacker transcripts
- Evaluator secrets: flags, execution tokens, verifier seeds
- API keys, `.env` files, cloud credentials
- Vendor binaries/firmware that are not redistributable

## Lab rules
- All execution happens in network-isolated, snapshot-and-rollback containers, VMs or emulators with no
  route to production systems or the internet.
- Builder tools are allowlisted and use only approved artifacts or controlled mirrors.
- Every target is human-reviewed before any attacker runs against it.
- Disclosed CVEs only. If an agent appears to find a **new** vulnerability, stop, record it privately,
  notify the mentor, and follow coordinated disclosure with the vendor.

## Release checklist (before making anything public)
- [ ] Mentor (Pat Engebretson) approves the release
- [ ] Repo scanned for secrets (`gitleaks detect`) and full git history checked
- [ ] Exploit artifacts removed, or replaced with redacted summaries (technique class, success/fail, cost)
- [ ] Any dataset of artifacts is access-gated (request form + research-use agreement), not public
- [ ] DSU IP/research policy confirmed for SRI-funded work
- [ ] Model provider usage policies reviewed for publication of results

## Reporting
Security issues with this repository: contact the maintainers privately; do not open a public issue.
