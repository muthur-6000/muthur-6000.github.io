---
title: "Infrastructure: Hardware Restoration of a Cisco UCS C220 M5 Server"
date: 2026-02-09 18:00:00 -0500
categories: [Systems-Infrastructure]
tags: [cisco, hardware-repair, proxmox, virtualization, raid, server-administration]
description: A technical walkthrough of recovering decommissioned enterprise hardware through physical jumper resets and firmware synchronization.
---

## Overview
This project involved the restoration and deployment of a decommissioned **Cisco UCS C220 M5** server. The unit was acquired in a locked state with unknown administrative credentials and outdated firmware, requiring a hardware-level bypass and a structured firmware update path to enable modern virtualization support.

## Technical Stack
* **Hardware:** Cisco UCS C220 M5 (LFF Chassis).
* **Management Interface:** Cisco Integrated Management Controller (CIMC) & vKVM.
* **Storage Controller:** Cisco 12G SAS Modular RAID Controller.
* **Drives:** 3x Toshiba PX05SMB040 12G SAS SSDs (RAID 5).
* **Hypervisor:** Proxmox VE 8.x.

## Technical Procedures

### 1. Administrative Credential Recovery (PWR REC)
Access to the BIOS and CIMC was restricted by forgotten passwords. To regain administrative control, I performed a hardware-level NVRAM clear.
* **Procedure:** Located the **Password Recovery Jumper (PWR REC)** on the motherboard. I moved the jumper from the default pins (1-2) to the recovery pins (2-3), cycled the system power to clear the persistent configuration, and returned the jumper to its original position.
* **Result:** Successfully reset the CIMC to factory defaults, allowing for the configuration of a new administrative account.



### 2. Firmware Lifecycle Management
The CIMC and BIOS firmware versions were significantly out of sync, causing stability issues with the SAS backplane. 
* **Update Path:** I utilized the Cisco Host Upgrade Utility (HUU) to perform a staged update to version 4.3.2. 
* **Validation:** Verified that the BIOS and CIMC were updated in tandem to maintain component compatibility and ensure the 10GbE network interfaces were correctly enumerated by the host OS.

### 3. Storage Architecture and RAID Configuration
The storage subsystem was architected for a balance of redundancy and write performance using enterprise SAS SSDs.
* **RAID Implementation:** Configured a **RAID 5** array using three 12G SAS SSDs. 
* **Controller Handshake:** Resolved a "Managed Mode" error that prevented the RAID controller from initializing. This required clearing the foreign configuration from the drives and forcing a fresh parity initialization via the vKVM Virtual Media mapping.

### 4. Virtualization and Network Logic
Post-hardware stabilization, Proxmox VE was deployed as the primary hypervisor.
* **Networking:** Configured Linux Bridges to isolate CIMC management traffic from the production VM VLANs.
* **Thermal Tuning:** Adjusted the fan profiles within the CIMC to "Low Power" mode to optimize for a homelab environment while maintaining safe operating temperatures for the dual-socket Xeon architecture.

## Outcome
The restoration resulted in a fully functional, high-density compute node. The unit currently serves as the primary virtualization host for testing complex network topologies and containerized services. The project demonstrates a systematic approach to enterprise hardware recovery, from physical board-level resets to logical OS optimization.
