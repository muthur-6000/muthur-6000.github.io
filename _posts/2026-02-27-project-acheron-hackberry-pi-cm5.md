---
title: "Project: Acheron—The Hackberry Pi CM5 Cyberdeck Build"
date: 2026-02-27 10:00:00 -0500
categories: [Enthusiast-Projects]
tags: [cyberdeck, hardware-modding, raspberry-pi, cm5, industrial-design, infrastructure]
description: Engineering a portable, industrial-grade terminal utilizing the Raspberry Pi CM5 and a tactile BB9900 physical interface.
---

## Overview
Project Acheron is a pursuit of tactile, high-performance mobile compute. While modern devices prioritize sleekness, this build focuses on "Cassette Futurism"—an aesthetic inspired by industrial utilitarianism and the **MU/TH/UR 6000** mainframe architecture. The project involves integrating a **Raspberry Pi CM5 Lite (8GB)** into a custom enclosure designed for network diagnostics, field-level troubleshooting, and terminal-heavy workflows.

## Technical Stack
* **Processor:** Raspberry Pi Compute Module 5 (CM5) Lite with 8GB RAM.
* **Storage:** High-speed NVMe via the CM5 PCIe interface (bypassing standard eMMC for superior I/O).
* **Input Interface:** BlackBerry 9900 (BB9900) QWERTY keyboard module.
* **OS:** Arch Linux (custom minimal configuration).
* **Chassis:** Custom industrial enclosure with integrated thermal management.

## The Engineering Plan

### 1. The Compute Core: CM5 Integration
The shift to the **CM5** architecture offers a significant performance uplift over the Pi Zero 2W or CM4.
* **Memory Management:** The 8GB RAM ensures that even with a heavy terminal loadout and background network scanners, the system remains responsive.
* **NVMe Storage:** By opting for the "Lite" module, I am bypassing the slower onboard eMMC to run the entire OS off an NVMe drive. This ensures enterprise-grade read/write speeds, critical for rapid diagnostic tool deployment.

### 2. Tactile Interface: The 9900 Keyboard
A cyberdeck is defined by its input. I have selected the **BB9900** keyboard for its legendary tactility.
* **Hardware Interfacing:** The keyboard requires a dedicated carrier board to translate the physical keystrokes into a signal the CM5 can process via I2C or USB. 
* **The Logic:** In field environments, a physical keyboard is superior to touch interfaces for entering complex terminal strings or managing remote server sessions.

### 3. Chassis Design and "Cassette Futurism"
The build will reject the "click-to-fix" aesthetic. The chassis will be modeled to feel like a piece of industrial equipment salvaged from a 1970s mainframe room.
* **Serviceability:** Following the mindset applied to my **[ThinkPad X13 Yoga]({% post_url 2026-02-01-thinkpad-x13-yoga-restoration %})** repairs, the enclosure will use standard fasteners to ensure 100% field serviceability.
* **Cooling:** Due to the CM5 power draw, a custom passive heatsink or low-profile active cooling solution will be integrated into the chassis to maintain peak clock speeds during high-density compute tasks.

### 4. OS Hardening and Custom Rice
The software environment will be a stripped-back Arch Linux installation.
* **Theme:** A monochrome green phosphor aesthetic, mirroring retro-terminal interfaces.
* **Tooling:** Pre-configured with a suite of infrastructure diagnostic tools, network scanners, and local knowledge vaults—bridging the gap between my **[Kiwix Knowledge Vault]({% post_url 2025-08-12-kiwix-offline-repository-deployment %})** and live system administration.

## Current Status: Procurement
As of February 2026, the primary components—including the CM5 and 9900 module—have been ordered. The project is currently in the **Logistics and Prototyping** phase. Once the hardware arrives, I will begin the initial stress testing and wiring of the carrier board.

## Outcome
The final result of Project Acheron will be a "zero-dependency" field terminal. By combining the latest Compute Module architecture with a legacy tactile interface, this build serves as a bridge between modern processing power and the reliable, physical UI of industrial computing history.
