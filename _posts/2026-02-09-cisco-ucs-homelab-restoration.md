---
title: "Infrastructure: Hardware Restoration of a Cisco UCS C220 M5 Server"
date: 2026-02-09 18:00:00 -0500
categories: [Systems-Infrastructure]
tags: [cisco, hardware-repair, proxmox, virtualization, raid, server-administration]
description: A technical walkthrough of recovering decommissioned enterprise hardware through physical jumper resets and firmware synchronization.
---

## Overview
This project involved the restoration and deployment of a decommissioned **Cisco UCS C220 M5** server. The unit was acquired in a locked state with unknown administrative credentials, requiring a hardware-level bypass and a structured firmware update path to enable modern virtualization support.

## Technical Stack
* **Chassis:** Cisco UCS C220 M5 (LFF).
* **Management Interface:** Cisco Integrated Management Controller (CIMC) & vKVM.
* **Storage Controller:** Cisco 12G SAS Modular RAID Controller.
* **Storage Inventory (Active Production):** 3x 744GB 12G SAS SSDs (Configured in RAID 5).
* **Storage Inventory (Unconfigured/Future NAS):** * 1x 557GB 10k SAS HDD.
    * 2x 371GB 12G SAS SSDs.
* **Hypervisor:** Proxmox VE 8.x.

## Technical Procedures

### 1. Administrative Credential Recovery (PWR REC)
Access to the BIOS and CIMC was restricted by forgotten passwords. To regain administrative control, I performed a hardware-level NVRAM clear.
* **Procedure:** Located the **Service Header Block J38** on the motherboard.
* **Action:** Utilized the jumper on Pins 1 and 2 to trigger a physical CMOS/Password reset, cycling system power to clear persistent configurations.
* **Result:** Successfully reset the CIMC to factory defaults, allowing for the configuration of a new administrative account.



### 2. Storage Architecture and RAID Configuration
The storage subsystem was architected for a balance of redundancy and write performance using enterprise SAS SSDs.



* **RAID Implementation:** Configured a **RAID 5** array using three identical 744GB SAS SSDs, providing a single-drive fault tolerance.
* **Inventory Management:** Retained an additional SAS HDD and two smaller SAS SSDs in an "Unconfigured Good" state, reserved for secondary storage pools or future NAS expansion.
* **Validation:** Utilized the Aptio Setup Utility to verify that the Virtual Disk status remained "Online" post-initialization.

### 3. Firmware Lifecycle Management
The CIMC and BIOS firmware versions were out of sync, requiring a staged update to maintain component compatibility.
* **Update Path:** Utilized the Cisco Host Upgrade Utility (HUU) to perform a staged update to version 4.3.2.
* **Outcome:** Ensured the 10GbE network interfaces were correctly enumerated by the host OS.

### 4. Virtualization and Network Logic
Post-hardware stabilization, Proxmox VE was deployed as the primary hypervisor.
* **Networking:** Configured Linux Bridges to isolate CIMC management traffic from production VM VLANs.
* **Thermal Tuning:** Adjusted fan profiles within the CIMC to "Low Power" mode to optimize for a homelab environment.

## Outcome
The restoration resulted in a fully functional, high-density compute node serving as the primary virtualization host. The project demonstrates a systematic approach to enterprise hardware recovery, from physical board-level resets to logical OS optimization.
