# Matter Ubuntu Lab — Reference Sources

Matter 관련 정보를 찾을 때 아래 우선순위를 따른다.

중요:
URL 자체를 정답으로 고정하지 않는다.

connectedhomeip 실험에서는
현재 checkout한 git revision의 code/docs가
웹의 최신 master보다 우선한다.

---

# 1. project-chip / connectedhomeip

Main Repository

https://github.com/project-chip/connectedhomeip

Matter 공식 open-source implementation의
주요 기술 기준.

---

## BUILDING Guide

https://github.com/project-chip/connectedhomeip/blob/master/docs/guides/BUILDING.md

사용 목적:

Ubuntu build environment
toolchain
bootstrap
activate
build 방법

실제 실험에서는 현재 checkout revision의
docs/guides/BUILDING.md를 우선한다.

---

## CHIP Tool Guide

https://github.com/project-chip/connectedhomeip/blob/master/docs/development_controllers/chip-tool/chip_tool_guide.md

사용 목적:

Commissioning
Fabric
Controller / Commissioner
Commissioning Window
Multi-Admin
alpha / beta commissioner
Command
Attribute read/write

Multi-Admin 실험의 최우선 참고자료.

---

# 2. Linux Matter Device

## Linux Lighting App

https://github.com/project-chip/connectedhomeip/blob/master/examples/lighting-app/linux/README.md

첫 Matter Device 후보.

Commissioning → OnOff Command → Attribute read 실습.

---

## Linux Simulated Device

https://github.com/project-chip/connectedhomeip/blob/master/docs/guides/simulated_device_linux.md

물리 Device 없이 Linux에서 Matter Device를
실험할 때 사용.

---

## All Devices App

https://github.com/project-chip/connectedhomeip/blob/master/examples/all-devices-app/README.md

여러 Device Type 및 bridged 기능을
검토할 때 참고.

---

# 3. Matter Bridge

## Linux Bridge App

https://github.com/project-chip/connectedhomeip/blob/master/examples/bridge-app/linux/README.md

Bridge
dynamic endpoint
bridged node
bridged endpoint

개념 및 구현 검토용.

중요:

README 명령을 기억에 의존해 실행하지 않는다.

현재 checkout revision에서
README
BUILD.gn
source tree
실제 target
이 일치하는지 확인한다.

Bridge는 기본 Device 및 Multi-Admin 성공 후 진행한다.

---

# 4. CSA Matter Specification

https://csa-iot.org/developer-resource/specifications-download-request/

필요할 때 확인할 자료:

Core Specification
Application Cluster Specification
Device Type Library
Namespace

사용 예:

Fabric 정의
Access Control
Bridged Node
Cluster mandatory/optional feature
Device Type 정의

Specification을 표준 자체의
규범적 기준(normative reference)으로 사용한다.

---

# 5. Matter 1.6

https://csa-iot.org/newsroom/matter-1-6-enables-more-intuitive-setup-multi-ecosystem-experiences-and-context-driven-control/

Multi-Admin과 Joint Fabric을 혼동하지 않기 위한 참고.

---

# 6. Nordic Semiconductor

Matter Fundamentals

https://academy.nordicsemi.com/courses/matter-fundamentals/

Nordic Documentation

https://docs.nordicsemi.com/

Nordic Product Information

https://www.nordicsemi.com/

사용 목적:

Matter 입문 개념
nRF5340
nRF54LM20
Matter over Thread
향후 실제 MCU 실험

Ubuntu PC-only 실험 명령은
connectedhomeip Linux 자료를 우선한다.

---

# 7. Espressif ESP-Matter

https://docs.espressif.com/projects/esp-matter/

향후 ESP32-C6 등 실제 Matter Device를
도입할 경우 참고한다.

---

# GitHub Issues 사용 규칙

connectedhomeip GitHub Issues는:

known bug
build regression
README 오류
현재 문서와 실제 구현 차이

를 찾는 보조자료로 사용한다.

Issue 하나의 주장을
Matter Specification 정의처럼 사용하지 않는다.

---

# Community source policy

Stack Overflow
Reddit
블로그
Medium
YouTube

등은 공식자료로 해결되지 않는
구체적인 문제의 보조자료로만 사용한다.

우선순위:

1. local connectedhomeip code
2. 같은 revision의 local docs
3. CSA specification
4. project-chip official material
5. Nordic/Espressif official docs
6. connectedhomeip Issues
7. community sources