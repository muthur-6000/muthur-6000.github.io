---
title: "Project: Programmatic Discovery of High-Value Usernames"
date: 2025-01-05 19:00:00 -0500
categories: [Enthusiast-Projects]
tags: [python, automation, web-scraping, requests, scripting, github]
description: Developing a custom Python-based tool to identify available short-character and "OG" handles across targeted web platforms.
---

## Overview
In the digital landscape, short-character (3-4 letter) or "OG" usernames are highly sought after but nearly impossible to find through manual searching. To address this, I developed a custom **Python-based Automation Script** designed to programmatically query registration endpoints and identify available handles in bulk.

## The Problem: The Efficiency Gap
Manually checking thousands of character permutations for availability is a terminal exercise in inefficiency. Most web platforms also implement basic rate-limiting or bot-detection to prevent exactly this kind of automated checking. 

My goal was to create a tool that was:
1. **Iterative:** Capable of generating thousands of unique character combinations based on specific constraints.
2. **Stealthy:** Able to mimic human browsing behavior to avoid IP-banning or 403 Forbidden responses.
3. **Performant:** Capable of logging "hits" to a local database for immediate verification.

## The Technical Methodology
The project was built using the **Python Requests** library, focusing on low-level HTTP status code analysis.

### 1. Permutation Logic
Rather than relying on a static wordlist, the tool utilizes a generator that iterates through character sets based on user input. This allows for targeted "hunts" (e.g., all possible 3-letter combinations with a specific starting character).



### 2. Request Handling & Bot Mitigation
To bypass standard rate-limiting, I implemented a randomized "sleep" logic and custom **User-Agent rotation**. By analyzing the difference between `404 Not Found` (often indicating availability) and `200 OK` (indicating a taken profile), the script filters through thousands of names without manual intervention.

## Outcome
This tool successfully identified multiple available three-character handles that had been "extinct" for years. It solidified my understanding of **asynchronous request handling**, **HTTP status codes**, and the nuances of **web-scraping ethics and mitigation bypass**.

The full source code, including the permutation engine and request handler, is available on my GitHub.

---

**[View the Source Code on GitHub](#)**
