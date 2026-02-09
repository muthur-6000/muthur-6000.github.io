---
title: "Proactive Systems Ops: Solving the M90 Tiny 'Invisible SSD' During Win 11 Migration"
date: 2025-07-15 15:00:00 -0500
categories: [Operations-Deployment]
tags: [sccm, imaging, windows-11, ubuntu, operations, bios, lenovo, deployment]
description: Proactively troubleshooting storage controller conflicts months ahead of the Windows 10 EOL deadline.
---

## Overview
With the **Windows 10 EOL (End of Life)** deadline approaching in October, I led a proactive push to migrate our fleet of **ThinkCentre M90 Tiny** PCs to Windows 11 Enterprise. By starting this migration in mid-2025, we aimed to ensure hardware stability and user adoption well before the security cutoff. However, the rollout hit an immediate technical snag: the **SCCM (MECM) Task Sequence** failed on several units because the target NVMe SSDs were invisible to the WinPE boot environment.

## The Technical Roadblock: Intel VMD vs. WinPE
In a high-volume deployment, any deviation from the standard hardware configuration can halt a project. Upon investigation, I found that while the units were identical in model, their storage controller configurations varied at the BIOS level.

### The Diagnostic Process
1.  **Hardware Verification:** Confirmed SSD presence in the BIOS/UEFI to rule out physical seating issues or DOA (Dead on Arrival) hardware.
2.  **Driver Isolation:** Verified that the SCCM boot image contained the latest Lenovo storage drivers. Since some units imaged successfully, the issue was isolated to a specific **per-device BIOS setting** rather than a global driver failure.
3.  **The Culprit:** The failing units were shipped with **Intel VMD (Volume Management Device)** enabled in RAID mode. Our standard WinPE environment was configured for AHCI, causing the "invisible drive" error.



## Technical Execution

### 1. Storage Controller Optimization
To allow the SCCM task sequence to communicate with the block storage, I had to manually intervene at the hardware level.
* **The Fix:** Switched the storage controller mode from RAID to **AHCI** and disabled the Intel VMD controller.
* **The Result:** The SSD was immediately recognized by the WinPE environment, allowing the disk partitioning and OS application steps to proceed without further error.

### 2. Standardizing the Deployment
To maintain the proactive timeline of the migration, I established a mandatory BIOS configuration checklist for all technicians involved in the rollout. This ensured that every M90 Tiny was "pre-staged" with AHCI settings before hitting the PXE boot stage, effectively eliminating the bottleneck for the remaining fleet.

## Outcome
By identifying and resolving the VMD/AHCI conflict months ahead of the Windows 10 EOL deadline, we maintained a smooth migration path. This proactive approach allowed us to address hardware-specific quirks in a controlled environment, ensuring the organization was fully compliant and secure well before the legacy OS reached its official sunset.

**Key Takeaway:** Real-world IT is about anticipation. By tackling the M90 Tiny storage conflicts in July, we avoided a high-pressure scramble in October.
