# Experiment 01 — Linux Matter Device

## Status

PASS

## Date

2026-08-29

## connectedhomeip

Tag: `v1.6.0.0`

Commit: `250a9e6c50ee2068107f3c4808b680f5f2925415`

## Goal

Ubuntu PC에서 물리 Matter 장비 없이 Linux virtual Matter Device를
빌드하고 실행한다.

## Build

    cd ~/connectedhomeip
    source scripts/activate.sh

    ./scripts/examples/gn_build_example.sh \
      examples/placeholder/linux \
      out/debug/simulated/ \
      chip_tests_zap_config=\"app1\"

Generated binary:

    out/debug/simulated/chip-app1

## Run

    ./out/debug/simulated/chip-app1 \
      --KVS ~/matter-ax-state/device-app1/chip_kvs \
      --passcode 20202021 \
      --discriminator 3842

## OBSERVED

- build completed successfully
- `chip-app1` was generated as an x86-64 ELF executable
- Matter server started successfully
- Matter service operated over IP/Ethernet
- commissionable-node advertisement was available
- Bluetooth/BlueZ initialization failed, but this did not stop IP operation

## INTERPRETATION

Ubuntu에서 실행되는 Linux process가 Matter Device 역할을 수행했다.

## NOT YET PROVEN

- physical Matter hardware
- Bluetooth commissioning
- application Cluster behavior

## Result

PASS
