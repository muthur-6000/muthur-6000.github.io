---
title: "Homelab Engineering: The $100 Minecraft Powerhouse"
date: 2026-01-10 12:00:00 -0500
categories: [Homelab]
tags: [lenovo, ubuntu-server, minecraft, fabric, webmin, amp, server-administration]
description: Repurposing a ThinkCentre M90 Tiny into a high-performance Fabric Minecraft server using Ubuntu Server and AMP.
---

## Overview
The goal of this project was to prove that enterprise-grade performance doesn't require enterprise-grade spending. Utilizing a decommissioned **Lenovo ThinkCentre M90 Tiny**—sourced for approximately **$140 CAD**—I architected a dedicated Minecraft server capable of handling a localized player base with high tick-rate stability.

## Technical Stack
* **Hardware:** Lenovo ThinkCentre M90 Tiny (Intel Core i5 / 16GB RAM / 256GB NVMe).
* **OS:** Ubuntu Server 24.04 LTS (Headless).
* **Management:** Webmin (System) & AMP by CubeCoders (Application).
* **Networking:** Playit.gg (Global Tunneling).
* **Game Engine:** Fabric MC (optimized with Lithium and Starlight).

## The Execution

### 1. OS Hardening & Remote Management
I initialized the project with a clean, headless installation of **Ubuntu Server**. To maintain the "Full Stack" management style without needing a physical monitor (crash-cart), I deployed **Webmin**. This allowed for browser-based terminal access, package management, and system health monitoring (CPU thermals and RAM utilization).

### 2. Application Layer: AMP & Fabric
For the game server orchestration, I utilized **AMP (Application Management Panel)**. 
* **Automation:** Configured automated backups and scheduled restarts to maintain JVM (Java Virtual Machine) heap health.
* **Optimization:** Deployed a **Fabric MC** instance. To maximize the M90 Tiny’s hardware, I integrated performance-mod clusters (Lithium/FerriteCore) to optimize server-side tick calculations and memory ballooning.

### 3. Networking: Bypassing CGNAT with Playit.gg
One of the primary hurdles in home-hosting is navigating ISP restrictions and Port Forwarding. 
* **The Logic:** I implemented **Playit.gg**, a global software-defined tunnel.
* **The Benefit:** By running the Playit agent at the OS level, I was able to assign a stable global IP to the server without exposing my home network via traditional port forwarding. This provided a secure, encrypted tunnel for external players to connect with minimal latency.

## Thermal & Power Efficiency
The M90 Tiny is an ultra-small-form-factor (USFF) node, making it highly efficient for 24/7 operation. 
* **Metrics:** The system draws minimal power at idle, costing less than **$2 CAD per month** to operate. 
* **Thermals:** Utilizing the internal blower fan, the system maintains a stable **65°C** under heavy chunk-rendering loads, ensuring no thermal throttling during peak gameplay.

## Outcome
The result is a low-latency, high-availability gaming node that rivals dedicated hosting providers costing $30+/month. This project demonstrates the value of **Hardware Repurposing**; by understanding the Linux stack and lightweight tunneling protocols, a "discarded" office PC can outperform modern consumer-grade hardware in specific server-side tasks.

**Key Takeaway:** Budget constraints are just engineering opportunities in disguise.
