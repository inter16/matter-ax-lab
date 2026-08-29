# Experiment 03 — Matter Data Model Discovery

## Status

IN PROGRESS

## Date

2026-08-29

## connectedhomeip

Tag: `v1.6.0.0`

Commit: `250a9e6c50ee2068107f3c4808b680f5f2925415`

## Goal

Commissioned Device의 실제 Matter 데이터 모델을 Device 자체에
질의하여 다음 구조를 확인한다.

    Device
    → Node
    → Endpoint
    → Device Type
    → Cluster
    → Attribute / Command / Event

## Current Device

Commissioner: `alpha`

Device Node ID: `1`

## Step 1 — Root Endpoint PartsList

Command:

    cd ~/connectedhomeip

    ./out/debug/chip-tool/chip-tool \
      descriptor read parts-list 1 0 \
      --commissioner-name alpha \
      --storage-directory ~/matter-ax-state/chip-tool

## OBSERVED

Descriptor Cluster:

    Endpoint: 0
    Cluster: 0x001D
    Attribute: 0x0003
    PartsList: 1 entries
    [1]: 1

## INTERPRETATION

Node ID `1` contains:

    Node 1
    ├── Endpoint 0
    └── Endpoint 1

Endpoint 0 is the Root Endpoint and its PartsList identifies Endpoint 1.

## NOT YET PROVEN

- Endpoint 0 Device Type
- Endpoint 1 Device Type
- Endpoint 0 Server/Client Cluster list
- Endpoint 1 Server/Client Cluster list
- supported Commands
- Events

## Next

Read `DeviceTypeList` from Endpoint 0.

## Result

IN PROGRESS

## Step 2 — Root Endpoint DeviceTypeList

Command:

    cd ~/connectedhomeip

    ./out/debug/chip-tool/chip-tool \
      descriptor read device-type-list 1 0 \
      --commissioner-name alpha \
      --storage-directory ~/matter-ax-state/chip-tool

### OBSERVED

Endpoint 0 Descriptor Cluster returned:

    Endpoint: 0
    Cluster: 0x001D
    Attribute: 0x0000
    DeviceTypeList: 2 entries

    DeviceType: 17 (Power Source)
    Revision: 1

    DeviceType: 22 (Root Node)
    Revision: 4

### INTERPRETATION

Endpoint 0 is the Root Endpoint and advertises both the Root Node and
Power Source node-scoped Device Types.

### NOT YET PROVEN

Endpoint 1 Device Type and its Cluster inventory remain unknown.

## Next

Read `DeviceTypeList` from Endpoint 1.

## Step 3 — Endpoint 1 DeviceTypeList

Command:

    cd ~/connectedhomeip

    ./out/debug/chip-tool/chip-tool \
      descriptor read device-type-list 1 1 \
      --commissioner-name alpha \
      --storage-directory ~/matter-ax-state/chip-tool

### OBSERVED

Endpoint 1 Descriptor Cluster returned:

    Endpoint: 1
    Cluster: 0x001D
    Attribute: 0x0000
    DeviceTypeList: 1 entries

    DeviceType: 257 (Dimmable Light)
    Revision: 3

Device Type 257 is `0x0101`.

### INTERPRETATION

Endpoint 1 is an application Endpoint implementing the
Dimmable Light Device Type.

### NOT YET PROVEN

The actual Server Clusters, Client Clusters, supported Commands,
Attributes, and Events on Endpoint 1 remain to be discovered.

## Next

Read `ServerList` from Endpoint 1.

## Step 4 — Endpoint 1 ServerList

Command:

    cd ~/connectedhomeip

    ./out/debug/chip-tool/chip-tool \
      descriptor read server-list 1 1 \
      --commissioner-name alpha \
      --storage-directory ~/matter-ax-state/chip-tool

### OBSERVED

Endpoint 1 Descriptor Cluster returned 10 Server Clusters:

    1106 (0x0452) ThreadBorderRouterManagement
    1030 (0x0406) OccupancySensing
      98 (0x0062) ScenesManagement
      65 (0x0041) UserLabel
      29 (0x001D) Descriptor
       4 (0x0004) Groups
       3 (0x0003) Identify
       6 (0x0006) OnOff
       8 (0x0008) LevelControl
     768 (0x0300) ColorControl

### INTERPRETATION

Endpoint 1 actually implements OnOff and LevelControl Server Clusters,
in addition to the other Server Clusters reported above.

Server Cluster presence proves that the Cluster is implemented on this
Endpoint, but does not yet prove successful Command execution.

### NOT YET PROVEN

- Client Cluster inventory
- individual Attribute inventory
- accepted/generated Commands
- Event inventory
- actual OnOff or LevelControl Command behavior
- full Device Type conformance

## Next

Read `ClientList` from Endpoint 1.

## Step 5 — Endpoint 1 ClientList

Command:

    cd ~/connectedhomeip

    ./out/debug/chip-tool/chip-tool \
      descriptor read client-list 1 1 \
      --commissioner-name alpha \
      --storage-directory ~/matter-ax-state/chip-tool

### OBSERVED

Endpoint 1 Descriptor Cluster returned 4 Client Clusters:

      3 (0x0003) Identify
      6 (0x0006) OnOff
      8 (0x0008) LevelControl
    768 (0x0300) ColorControl

### INTERPRETATION

Endpoint 1 declares client-side support for Identify, OnOff,
LevelControl, and ColorControl.

Client Cluster presence does not prove that the application has
actually sent Commands to another Matter Endpoint.

### NOT YET PROVEN

- Endpoint 0 Server/Client Cluster inventory
- individual Attribute inventory
- accepted/generated Commands
- Event inventory
- actual application Cluster behavior

## Next

Read the Root Endpoint ServerList.
