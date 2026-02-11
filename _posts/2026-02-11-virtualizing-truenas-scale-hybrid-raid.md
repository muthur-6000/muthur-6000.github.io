---
title: "Homelab: Architecting TrueNAS Scale on Cisco UCS (The Hybrid RAID Strategy)"
date: 2026-02-11 13:25:00 -0500
categories: [Systems-Infrastructure]
tags: [truenas, zfs, proxmox, io-optimization, cisco-ucs, storage-architecture, virtio]
description: A deep-dive into configuring ZFS on enterprise hardware without an HBA, utilizing a "Hybrid Redundancy" topology and specific Proxmox I/O threading optimizations.
---

## Overview
The "standard" advice for TrueNAS is simple: pass through a raw HBA (IT Mode) and let ZFS manage the physical disks. However, working with a **Cisco UCS C220 M5** and its integrated **12G SAS RAID Controller** presented a constraint: the controller does not support a simple "JBOD" passthrough mode for ZFS without significant firmware hacking.

This project focused on architecting a stable, high-performance **"Hybrid Redundancy"** solution: leveraging the Cisco hardware RAID for physical drive protection while virtualizing TrueNAS Scale for logical volume management.

## The "Hybrid" Storage Topology
Running ZFS on top of a Hardware RAID is often considered "illegal" in homelab circles due to the risk of write-cache corruption. To make this safe and performant, I implemented a specific multi-layer architecture:

### 1. Physical Layer (Cisco RAID 1) 
* **Configuration:** 2x 600GB SAS SSDs configured in **Hardware RAID 1** via the Cisco CIMC.
* **The Logic:** This handles the *physical* redundancy. If a drive fails, the Cisco controller handles the rebuild invisibly to the OS.

### 2. Virtual Layer (VirtIO SCSI)
* **Configuration:** This RAID 1 volume was presented to Proxmox as a single storage block, then carved out as a **VirtIO SCSI** virtual disk for the TrueNAS VM.
* **The "Trouble":** By default, Proxmox creates disk images with write-caching enabled. If the host loses power, the data in the RAM cache is lost before it hits the hardware RAID controller, leading to ZFS pool corruption.

## Critical Troubleshooting & Optimization
To prevent the "Write Hole" and ensure the VM didn't lock up the host CPU during heavy transfers, specific I/O tuning was required.

### The "No Cache" Safety Valve
I explicitly configured the Virtual Hard Disk cache to **"Default (No Cache)"**.
* **The Fix:** This forces all write operations to bypass the host RAM and commit directly to the persistent storage.
* **The Result:** While this incurs a slight latency penalty, it guarantees that when ZFS thinks a block is written, it is physically safe on the SAS SSDs—critical for preventing pool degradation during power events.

### The "IO Thread" Lockup Fix
During initial testing, heavy SMB transfers (large backups) would cause the entire Proxmox host UI to stutter.
* **The Diagnosis:** The heavy I/O interrupts were flooding the main QEMU process loop.
* **The Fix:** Enabling **"IO Thread"** on the disk controller settings.
* **The Outcome:** This offloads disk I/O processing to a dedicated worker thread, separate from the main VM execution loop. Throughput stabilized, and host CPU usage dropped by ~15% during active writes.

### The Memory War (ARC vs Ballooning)
ZFS is designed to consume all available RAM for its **Adaptive Replacement Cache (ARC)**.
* **The Conflict:** Proxmox's "Memory Ballooning" driver attempts to reclaim unused RAM from VMs. Since ZFS marks its ARC as "used," the balloon driver fights ZFS, causing massive swap thrashing.
* **The Resolution:**
    1.  **Fixed Allocation:** Assigned **16GB DDR4** strictly to the VM.
    2.  **Ballooning Disabled:** Unchecked "Ballooning Device" in Proxmox hardware settings. This physically reserves the memory addresses for the VM, preventing the hypervisor from ever attempting to reclaim them.

## Outcome
This configuration delivers the best of both worlds: **Hardware-level drive replacement** (hot-swapping SAS drives via Cisco) and **Software-level dataset management** (Snapshots, Replication via TrueNAS). The system sustains **Gigabit line-speed** (115MB/s) on SMB transfers with zero host-level stuttering.
