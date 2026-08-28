# matter-ax-lab

Ubuntu PC에서 Matter를 처음부터 실제로 실행하고 검증하며,
AI@Home matter AX Sprint 2026을 위한 재현 가능한 프로토타입 기반을 구축하는 실험 저장소입니다.

## Current Tested Baseline

connectedhomeip:

- Tag: `v1.6.0.0`
- Commit: `250a9e6c50ee2068107f3c4808b680f5f2925415`

Verified:

- Linux simulated Matter Device: PASS
- CHIP Tool build: PASS
- First commissioning with commissioner `alpha`: PASS
- Operational CASE reconnect: PASS
- Basic Information / VendorID attribute read: PASS
- OnOff command: NOT YET TESTED
- Multi-Admin alpha/beta: NOT YET TESTED
- Matter Bridge: NOT YET TESTED

## Repository Layout

- `docs/` — environment, upstream baseline, experiment summary, project goals, references
- `experiments/` — reproducible evidence and notes for individual Matter experiments
- `scripts/` — repeatable experiment/build/control scripts
- `src/` — project-specific controller, bridge, and local decision/AI code

## Repository Boundaries

This repository contains our experiment code and reproducibility records.

The upstream Matter SDK is kept separately in:

`~/connectedhomeip`

Matter runtime state and Fabric credentials are kept outside Git in:

`~/matter-ax-state`

Do not commit Fabric credentials, KVS files, private keys, passwords,
Wi-Fi credentials, or unnecessary personal/network information.

## Current Direction

The next technical work is to inspect the commissioned virtual device:

Device → Node → Endpoint → Device Type → Cluster → Attribute / Command / Event

After the basic Cluster experiments are stable, the project proceeds to
Multi-Admin, state synchronization, Matter Bridge, and local decision logic.
