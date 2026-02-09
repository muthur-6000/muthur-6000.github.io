---
title: "Operations & Logistics: 2026 Enterprise iPad Refresh (240+ Units)"
date: 2026-02-05 10:00:00 -0500
categories: [Operations-Deployment]
tags: [project-management, m365, intune, ios, logistics, veeva]
description: Orchestrating a 240-unit national hardware rollout involving complex CRM integrations and automated logistics.
---

## Overview
A national hardware rollout is a test of both technical infrastructure and organizational logistics. This project involved the strategic refresh of **240+ legacy iPad units** for a diverse Canadian workforce, ranging from local hybrid office staff to field-based CRM (Customer Relationship Management) teams. 

The primary drivers for this refresh were the conclusion of the legacy hardware lifecycle and mandatory top-down integration changes within the **Veeva** platform, which required the enhanced processing power and security architecture of the newer **iPad Air** models.

## The Strategy: Process Automation
To manage a rollout of this scale without ballooning help desk tickets, I architected an automated logistics workflow using the **Microsoft 365 stack**:

1.  **Data Collection (MS Forms):** Designed a national logistics form to capture critical user data: current asset tags, precise shipping coordinates for field employees, and departmental cost centers.
2.  **Workflow Logic (MS Approvals):** Integrated an automated approval chain. This ensured that every unit shipped was verified by departmental leadership, maintaining strict financial governance.
3.  **Stakeholder Alignment:** Acted as the primary Canadian technical lead, coordinating deployment schedules with US-based Operations management and local leadership to ensure zero downtime for field teams.



## Technical Execution

### 1. Zero-Touch Enrollment & Self-Service
Managing 240 units manually is impossible. I utilized **Apple’s Device Enrollment Program (DEP)** and **Microsoft Intune** to achieve a "Zero-Touch" experience:
* **Automated Provisioning:** Devices were configured to automatically pull corporate security policies and Wi-Fi certificates the moment they were unboxed.
* **Company Portal & Licensing:** Rather than forced pushes, I managed the deployment of the **Intune Company Portal**. This empowered users to self-install required tools while utilizing a **pool-based licensing model**. This ensured that high-value licenses (like Veeva integrations) were dynamically allocated to active users, optimizing costs through "last-seen" seat rotation.

### 2. Physical Logistics & IMAC/R
The **IMAC/R** (Install, Move, Add, Change, Remove) phase required precise physical coordination:
* **Asset Mapping:** Every new iPad Air was mirrored in our inventory system, linking the new serial numbers to the correct user profiles.
* **Legacy Recovery:** Established a secure "Return to Base" (RTB) workflow for decommissioned units, ensuring data sanitization and sustainable hardware disposal.

## Communication & Adoption
To bridge the gap between IT and the business, I utilized my **Business Communications** background to develop a high-impact "Migration Kit":
* **Visual Documentation:** Designed "Quick Start" adoption guides using **Adobe Photoshop** and **Illustrator**. These guides translated complex migration steps (e.g., iCloud backups and MFA enrollment) into accessible, visual instructions.
* **Proactive Support:** Drafted targeted communications for managers, outlining the technical prerequisites to ensure their teams were prepared for the transition.

## Outcome
By replacing manual spreadsheet tracking with **Microsoft Forms** and automated workflows, administrative overhead was reduced by approximately **40%**. The rollout successfully modernized the Canadian iPad fleet, providing the field teams with the hardware necessary to support the latest CRM integrations while significantly hardening our mobile security posture.

This project stands as a benchmark for how **structured data and clear communication can turn a complex logistics hurdle into a seamless operational upgrade.**
