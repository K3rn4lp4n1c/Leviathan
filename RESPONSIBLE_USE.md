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


## Reporting
Security issues with this repository: contact the maintainers privately; do not open a public issue.
