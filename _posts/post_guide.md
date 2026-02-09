**Project Posting Guide**
1. File Location and Naming
All project files must be stored in the /_posts directory. Files must follow this exact naming convention to be recognized by the site engine:

YYYY-MM-DD-title-of-project.md

Example: 2026-02-09-cisco-ucs-rebuild.md

2. Front Matter Template
Every post must begin with a YAML block at the top of the file. Copy and paste this template:

Markdown
---
title: "Title of Project"
date: YYYY-MM-DD HH:MM:SS -0500
categories: [Category1, Category2]
tags: [tag1, tag2]
description: A short one-sentence summary for the preview card.
---

Rules for Front Matter:

Categories: Use only 1 or 2 high-level categories (e.g., Infrastructure, Operations, AV-Engineering).

Tags: Use specific technologies (e.g., Proxmox, Q-SYS, PowerShell).

Dates: Use the -0500 suffix for Eastern Standard Time.

3. Image Handling
Store all project-related images in /assets/img/. To display them in a post, use standard Markdown syntax:

![Alt Text](/assets/img/filename.jpg)

4. Writing Content
Use Markdown headers to structure the project for readability:

## Overview: The problem or goal.

## Technical Stack: Hardware and software used.

## Execution: Steps taken to complete the project.

## Outcome: The final result or lessons learned.

5. Verification
After committing a new post, check the Actions tab on GitHub.

Green Check: The post is live.
Red X: Check for syntax errors in the Front Matter (ensure colons have a space after them).
