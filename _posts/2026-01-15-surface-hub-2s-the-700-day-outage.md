---
title: "Operations: The 700-Day Outage — A Forensic Recovery Saga"
date: 2026-01-15 11:00:00 -0500
categories: [Operations-Deployment]
tags: [microsoft, surface-hub, mtr, vendor-management, forensic-recovery, project-management, troubleshooting]
description: Breaking a multi-year failure loop by bypassing vendor misdirection and UEFI-level migration conflicts.
---

## Overview
When I joined the organization in July 2024, I inherited a **Microsoft Surface Hub 2S** that was effectively a very expensive piece of wall art. It had been non-functional since before my arrival—totaling over 700 days of downtime. Despite being a flagship asset in the executive boardroom, it had fallen through the cracks of organizational metrics, likely because it was never properly enrolled in Intune or was intentionally ignored to avoid tanking UCC performance data. 

This is the documentation of how I broke an 18-month vendor stalemate, bypassed a third-party support loop in Nicaragua, and finally forced a resolution from Microsoft’s US Head Office.

## The Cycle of Insanity (July 2024 – August 2025)
For the first year, I followed the "established" protocols. The device would be "fixed" by a technician, it would work for two weeks, and then—predictably—it would collapse back into a BitLocker recovery screen or a terminal Blue Screen of Death (BSOD). 

### The Hardware Misdirection
In early 2025, Microsoft Support recommended a physical SSD re-image. They even provided a specific list of third-party "mandated" hardware, including the **StarTech USB312SAT3CB** USB-to-SATA adapter. 
* **The Procurement:** I sourced the $20 adapter and notified support.
* **The Realization:** Upon receiving the "official" guide, I discovered it was for the **Surface Hub V1**. Our unit was a **2S**, which utilizes a modular compute cartridge and lacks the external SSD hatch described in the documentation. 

This was the first major red flag: the vendor didn't even know which hardware revision they were troubleshooting.

## The 88% Wall: Forensic Surveillance (November 2025)
By late 2025, the fleet-wide migration to **Windows 11 IoT** was underway. Out of 300+ units, this device (and a few other "stragglers") became a terminal failure point. The migration launcher would execute, initialize, and then consistently hard-crash at exactly **88% completion**.

### High-Speed Video Diagnostics
Standard logging failed to capture the crash—the unit would flash a BSOD and reboot faster than the human eye could process. 
* **The Hack:** I staged a tripod and an **iPhone** set to high-frame-rate video to surveil the screen during the migration.
* **The Evidence:** By scrubbing the footage frame-by-frame, I captured the stop code: **MEMORY_MANAGEMENT**. 
* **The Logic:** Further investigation of the **Event Viewer** revealed thousands of entries for this specific stop code. We weren't fighting a software bug; we were fighting a UEFI-level memory allocation conflict that triggered only during the kernel transition.

## The Handoff: Nicaragua to Redmond (December 2025)
After providing the forensic video evidence and the Event Viewer logs, I forced the ticket out of the hands of the offshore support team (Concentrix, Nicaragua). 
* **The "Ghost" Call:** Out of the blue, I received a direct Teams call from a US-based Microsoft manager. 
* **The Admission:** He admitted he had inherited the ticket and found it to be a complete mess—there were **zero internal notes** from the previous 18 months of support cycles. He was baffled as to how a flagship asset could be left in this state for so long.
* **The $779 USD Gambit:** Initially, support tried to quote **$779 USD (~$1,050 CAD)** for an on-site swap via UNISYS, despite the unit being out of warranty since 2020. However, after presenting my timeline and the evidence of vendor misdirection, the manager pushed through a resolution that finally stabilized the unit.

## The Final Reset: SEMM and Stability
As a last-ditch effort before the hardware swap, we attempted a manual UEFI hardening process using a **Surface Enterprise Management Mode (SEMM)** certificate. 
* **The Success:** While the "cursed" unit still struggled, the SEMM method successfully cleared 10 other "straggler" units in the fleet.
* **The Outcome:** By being the only person to consistently respond while everyone else was "at the water cooler," I forced a definitive resolution. The unit was eventually stabilized with a fresh SSD cartridge and a clean Windows 11 IoT build.

## Key Takeaways
1. **Persistence is a Technical Skill:** Technical knowledge is useless if you don't have the grit to stay on a ticket for 18 months.
2. **Document Everything:** The only reason I won the argument with Microsoft Head Office was because I had the receipts, the iPhone footage, and the timeline.
3. **Vendor Accountability:** Just because a rep has a "Microsoft" badge doesn't mean they are giving you the right documentation. Always verify the hardware revision.

---

**Status:** Production Stable (January 2026)
**Total Downtime:** ~740 Days
**Resolution:** Successful migration to Windows 11 IoT / MTR Pro.
