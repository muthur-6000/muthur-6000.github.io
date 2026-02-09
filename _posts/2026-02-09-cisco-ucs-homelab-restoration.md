---
title: "Full-Stack Infrastructure: Cisco UCS C220 M5 Restoration"
date: 2026-02-09 14:00:00 -0500
categories: [Infrastructure, Homelab]
tags: [cisco, proxmox, virtualization, raid, hardware-repair]
description: A complete vertical restoration of enterprise rack hardware into a high-density Proxmox hypervisor.
---

## Overview
This project involved the "Full Stack" restoration of a decommissioned **Cisco UCS C220 M5** server. The goal was to bridge the gap between enterprise-grade hardware and home lab utility, creating a stable, high-performance environment for virtualization and network testing.

## Technical Stack
* **Hardware:** Cisco UCS C220 M5 Rack Server.
* **Storage:** 12G SAS SSDs in a RAID 5 configuration.
* **Firmware:** Cisco Integrated Management Controller (CIMC).
* **Hypervisor:** Proxmox VE (Debian-based).
* **Power:** APC Smart-UPS redundancy.



## Execution

### Phase 1: The Physical Layer
The foundation of the project required sourcing and installing enterprise-spec SAS SSDs. I handled the hardware integration, including drive caddy installation and physical seating within the chassis.

### Phase 2: Firmware & RAID Architecture
Utilizing the **CIMC (Cisco Integrated Management Controller)**, I performed a full audit of the system firmware.
* **Firmware Updates:** Patched BIOS and controller firmware to ensure compatibility with modern hypervisors.
* **RAID Configuration:** Architected a **RAID 5** array using the onboard 12G SAS controller. This configuration was selected to provide an optimal balance between storage capacity, read/write performance, and data redundancy.

### Phase 3: Virtualization Layer
With the hardware stabilized, I deployed **Proxmox VE**. 
* **Tuning:** Optimized the hypervisor settings for the UCS architecture, including CPU pinning and memory ballooning for guest VMs.
* **Service Delivery:** Initialized a series of LXC containers and Virtual Machines to handle local network services and development sandboxes.

## Outcome
The result is a production-grade hypervisor node running in a personal lab environment. By managing the vertical from the physical SSD installation up to the hypervisor service layer, I successfully bypassed the need for third-party integration and created a cost-effective, high-availability server solution.

Lessons learned included the critical importance of maintaining **APC UPS** backups during RAID initialization to prevent parity errors during potential power fluctuations.
