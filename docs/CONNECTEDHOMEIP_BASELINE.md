# ConnectedHomeIP Tested Baseline

## Upstream

project-chip/connectedhomeip

## Tested Revision

Branch: detached HEAD (tag checkout)

Commit:
250a9e6c50ee2068107f3c4808b680f5f2925415

Tag:
v1.6.0.0

Date:
2026-08-29

## Environment

Ubuntu:
24.04.4 LTS

Architecture:
x86_64

Python:
3.12.3

## Verified Experiments

Linux Matter Device:
PASS

CHIP Tool:
PASS

Commissioning:
PASS

Operational CASE reconnect:
PASS

OnOff Command:
NOT YET TESTED

Attribute Read:
PASS
- Basic Information / VendorID
- Node ID: 1
- Endpoint: 0
- Observed value: 65521 (0xFFF1)

Multi-Admin alpha/beta:
NOT YET TESTED

Bridge:
NOT YET TESTED

## Baseline Applications

Linux simulated Matter Device:
examples/placeholder/linux
chip_tests_zap_config="app1"

Device binary:
out/debug/simulated/chip-app1

Controller:
examples/chip-tool

CHIP Tool binary:
out/debug/chip-tool/chip-tool

## Fabric Baseline

Commissioner:
alpha

Device Node ID:
1

First Fabric commissioning:
PASS

## Important Rule

Subsequent experiments default to this revision.

Do not silently update connectedhomeip master.

CHIP Tool and test Device should use this same revision unless a specific
experiment requires otherwise.

If an upgrade is necessary:

1. explain why
2. create a separate branch or separate checkout
3. rerun regression tests
4. update this document only after successful verification
