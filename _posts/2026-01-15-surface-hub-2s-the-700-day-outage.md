---
title: "Operations: The 700-Day Outage — A Forensic Recovery Saga"
date: 2026-01-15 11:00:00 -0500
categories: [Operations-Deployment]
tags: [microsoft, surface-hub, mtr, vendor-management, forensic-recovery, project-management, troubleshooting]
description: Breaking a multi-year failure loop by bypassing vendor misdirection and proving technical persistence through malicious compliance.
---

## Overview
When I joined the organization in July 2024, I inherited a **Microsoft Surface Hub 2S** that had been non-functional since before my arrival—totaling over 700 days of downtime. This project involved breaking an 18-month vendor stalemate and bypassing a third-party support loop in Nicaragua. More importantly, it required using forensic surveillance to debunk internal theories and force a resolution from Microsoft’s US Head Office.

## The Cycle of Insanity (July 2024 – August 2025)
The device would be "fixed," work for two weeks, and then collapse back into a BitLocker recovery screen. For a year, I was stuck in a loop of standard protocols that were clearly failing to address the root cause.

### The SATA Adapter Gaslight
In early 2025, Microsoft Support mandated the purchase of a specific third-party hardware part to re-image the SSD directly: the **StarTech USB312SAT3CB** USB-to-SATA adapter. 
* **The Procurement:** I sourced the $20 adapter immediately.
* **The Misdirection:** Upon receiving the "official" re-imaging guide, I discovered it was for the **Surface Hub V1**. Our unit was a **2S**, which has no external SSD hatch. 
* **The Response:** When I pointed out the hardware mismatch, Support never acknowledged the error. They simply moved the goalposts and asked me to "try re-imaging again" via standard USB, completely ignoring the fact that they had just directed me to buy unnecessary hardware.

## Malicious Compliance: The iPhone Surveillance
By late 2025, the migration to **Windows 11 IoT** was failing at exactly **88%**. Internal UCC teams were certain the failure was due to user error, claiming I "wasn't sticking around to tap the screen" to prevent the device from sleeping during the recovery. 



### The Alibi Camera
I knew that a device being recovered at the UEFI/BMR level wouldn't have "sleep timer" issues, but to silence the critics, I turned to **Malicious Compliance**.
* **The Setup:** I staged a tripod and an **iPhone** to record the entire process.
* **The Proof:** I recorded myself standing by the unit for hours, physically tapping the screen every 4–5 minutes to satisfy the UCC team's theory. 
* **The "I Told You So":** When the unit inevitably crashed at 88% despite my constant presence, I didn't just have a failed migration—I had forensic video evidence. By scrubbing the footage, I captured the momentary **MEMORY_MANAGEMENT** stop code that was invisible to the naked eye.

## The Handoff: Nicaragua to Redmond (December 2025)
After providing the forensic video evidence and the Event Viewer logs (which showed thousands of entries for the memory stop code), I forced the ticket out of the offshore support team (Concentrix, Nicaragua). 

* **The "Ghost" Call:** I received a direct Teams call from a US-based Microsoft manager who had inherited the "ghost" ticket. 
* **The Admission:** He admitted there were **zero internal notes** from the previous 18 months. My documented timeline and video evidence were the only reliable records of the device's history. 
* **The Resolution:** After trying to quote an **$800 USD** on-site swap for an out-of-warranty device, Microsoft finally acknowledged the systemic support failure and covered the resolution to get the unit back into production.

## Key Takeaways
1. **Malicious Compliance as a Tool:** Sometimes you have to film yourself doing "silly" tasks to prove they aren't the solution.
2. **Vendor Accountability:** Don't let support move the goalposts when they give you the wrong documentation.
3. **Forensic Persistence:** A $10,000 asset was saved because one person was willing to record a screen for hours to find a single frame of data.

---

**Status:** Production Stable (January 2026)
**Total Downtime:** ~740 Days
**Resolution:** Successful migration to Windows 11 IoT / MTR Pro.
