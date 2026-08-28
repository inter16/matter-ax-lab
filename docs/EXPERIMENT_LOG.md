# Matter Experiment Log

==================================================
Experiment 00 — Environment Check
==================================================

Date:
2026-08-29

Goal:
Identify the Ubuntu build environment before Matter setup.

Environment:
Ubuntu 24.04.4 LTS
x86_64
Kernel 7.0.0-28-generic
Python 3.12.3
Git 2.43.0
GCC/G++ 13.3.0

Observed:
Ubuntu environment and available resources were identified.
No Bluetooth HCI interface was observed.
bluetooth.service was inactive.

Result:
PASS

Interpretation:
The Ubuntu development environment was identified and documented.

Not Yet Proven:
Matter build readiness was not proven by this experiment alone.

Problems:
Bluetooth HCI was not available.

Resolution:
No action required for the initial Ethernet/IP Matter experiments.

Git commit:
PENDING — first baseline checkpoint


==================================================
Experiment 01 — Linux Matter Device
==================================================

Date:
2026-08-29

Goal:
Build and run a virtual Matter Device on Ubuntu.

connectedhomeip revision:
Tag: v1.6.0.0
Commit: 250a9e6c50ee2068107f3c4808b680f5f2925415

Commands:

source scripts/activate.sh

./scripts/examples/gn_build_example.sh \
  examples/placeholder/linux \
  out/debug/simulated/ \
  chip_tests_zap_config=\"app1\"

./out/debug/simulated/chip-app1 \
  --KVS ~/matter-ax-state/device-app1/chip_kvs \
  --passcode 20202021 \
  --discriminator 3842

Expected:
chip-app1 builds and starts as a Matter server.

Observed:
GN generation completed.
Ninja completed 843/843 targets.
chip-app1 was generated as an x86-64 ELF executable.
Matter server initialization completed.
UDP/TCP port 5543 was opened.
Commissionable-node mDNS advertisement was published.
Ethernet interface was detected.

Bluetooth/BlueZ initialization failed and CHIPoBLE was disabled.
The Matter server continued running over IP.

Result:
PASS

Interpretation:
A Linux process on the Ubuntu PC operated as a virtual Matter Device.

Not Yet Proven:
Physical Matter hardware behavior.
Bluetooth commissioning.
Cluster application behavior.

Problems:
BlueZ service activation timed out.

Resolution:
Use on-network IP commissioning for the current PC-only experiment.

Git commit:
PENDING — first baseline checkpoint


==================================================
Experiment 02 — CHIP Tool and First Commissioning
==================================================

Date:
2026-08-29

Goal:
Build CHIP Tool from the same revision and commission chip-app1.

connectedhomeip revision:
Tag: v1.6.0.0
Commit: 250a9e6c50ee2068107f3c4808b680f5f2925415

Commands:

./scripts/examples/gn_build_example.sh \
  examples/chip-tool \
  out/debug/chip-tool

./out/debug/chip-tool/chip-tool \
  pairing onnetwork-long 1 20202021 3842 \
  --commissioner-name alpha \
  --storage-directory ~/matter-ax-state/chip-tool

Expected:
CHIP Tool discovers the device and commissions Node ID 1.

Observed:
CHIP Tool built successfully.
PASE / SPAKE2+ succeeded.
Device attestation and operational credential provisioning completed.
NOC was installed on the device.
CASE establishment succeeded.
CommissioningComplete returned success.
Device Node ID 1 became an operational Matter node.
Device-side Fabric Index 1 was created.

Result:
PASS

Interpretation:
The virtual Matter Device joined the first Matter Fabric managed by
commissioner alpha.

Not Yet Proven:
Application Cluster command behavior.
Multi-Admin.
Second Fabric.
State synchronization.

Problems:
No blocking commissioning error observed.

Resolution:
None required.

Git commit:
PENDING — first baseline checkpoint


==================================================
Experiment 03 — Operational CASE and Attribute Read
==================================================

Date:
2026-08-29

Goal:
Verify that a new CHIP Tool process can reload alpha Fabric state,
establish CASE, and read an Attribute from Node ID 1.

Command:

./out/debug/chip-tool/chip-tool \
  basicinformation read vendor-id 1 0 \
  --commissioner-name alpha \
  --storage-directory ~/matter-ax-state/chip-tool

Expected:
CASE session succeeds and VendorID is returned.

Observed:
Fabric index 1 was restored from persistent CHIP Tool storage.
Operational discovery found Device Node ID 1.
CASE Sigma1/Sigma2/Sigma3 completed successfully.
Basic Information Cluster VendorID was read from Endpoint 0.

Observed VendorID:
65521 (0xFFF1)

Result:
PASS

Interpretation:
The commissioned alpha Fabric credentials remained usable after the
commissioning command exited, and operational Matter communication worked.

Not Yet Proven:
OnOff Command.
Writable Attribute behavior.
Endpoint / Device Type / Cluster inventory.
Events and subscriptions.

Problems:
Multiple host network interfaces were visible during operational discovery,
but the read completed successfully.

Resolution:
No action required at this point.

Git commit:
PENDING — first baseline checkpoint


==================================================
Experiment 04 — Multi-Admin alpha / beta
==================================================

Result:
NOT YET TESTED


==================================================
Experiment 05 — State Synchronization
==================================================

Result:
NOT YET TESTED


==================================================
Experiment 06 — Matter Bridge
==================================================

Result:
NOT YET TESTED


==================================================
Experiment 07 — Bridged Endpoint
==================================================

Result:
NOT YET TESTED


==================================================
Experiment 08 — Local Decision → Matter
==================================================

Result:
NOT YET TESTED
