# Experiment 02 — First Commissioning

## Status

PASS

## Date

2026-08-29

## connectedhomeip

Tag: `v1.6.0.0`

Commit: `250a9e6c50ee2068107f3c4808b680f5f2925415`

## Goal

같은 connectedhomeip revision에서 빌드한 CHIP Tool을 사용하여
Linux virtual Matter Device를 첫 Fabric에 Commissioning한다.

## Commissioner

Name: `alpha`

Device Node ID: `1`

## Command

    cd ~/connectedhomeip

    ./out/debug/chip-tool/chip-tool \
      pairing onnetwork-long 1 20202021 3842 \
      --commissioner-name alpha \
      --storage-directory ~/matter-ax-state/chip-tool

## OBSERVED

- PASE / SPAKE2+ succeeded
- device attestation succeeded
- operational credentials were provisioned
- NOC was installed on the Device
- CASE establishment succeeded
- CommissioningComplete returned success
- Device-side Fabric Index `1` was created

A later independent CHIP Tool process restored the alpha Fabric state,
established a new CASE session, and read:

    Node ID: 1
    Endpoint: 0
    Cluster: Basic Information
    Attribute: VendorID
    Value: 65521 (0xFFF1)

## INTERPRETATION

The Device joined alpha's Matter Fabric, and the stored operational
credentials remained usable after the commissioning process exited.

## NOT YET PROVEN

- OnOff Command
- writable Attribute
- complete Endpoint / Cluster structure
- second Fabric
- Multi-Admin
- state synchronization

## Evidence

- [`logs/chip-tool-build.txt`](logs/chip-tool-build.txt)
- [`logs/commissioning-alpha.txt`](logs/commissioning-alpha.txt)
- [`logs/post-commission-vendor-id.txt`](logs/post-commission-vendor-id.txt)

The evidence files are curated extracts from terminal output observed during the experiment; they are not represented as byte-for-byte raw terminal captures.

## Result

PASS
