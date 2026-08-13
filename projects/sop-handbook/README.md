# Security Operations SOP Handbook

A growing collection of standardized forms and procedures for documenting security
work. This handbook is my own initiative to bring consistency, repeatability, and a
document-control mindset to how I record labs, investigations, and technical tasks.

## Why this exists
It started small: while documenting my lab work I noticed my write-ups were more
useful when they followed a consistent incident-report structure. That turned into a
reusable template, then a controlled form with a document ID, and then the larger
idea — that a set of standardized forms plus the procedures for using them is exactly
how a security team keeps its documentation auditable and repeatable across people.
So I began building one, starting with the first form.

## Contents

| ID | Title | Purpose |
|----|-------|---------|
| [SOP-001](./SOP-001-handbook-overview.md) | Handbook Overview and Document Usage | Read this first — the index and usage guide for the handbook |
| [FORM-001](./FORM-001-writeup.md) | Technical / Incident Write-Up | Document incidents, lab exercises, and technical tasks |
| [FORM-002](./FORM-002-study-analysis.md) | Event / Study Analysis | Document study sessions — Messer videos, TryHackMe rooms |
| [FORM-003](./FORM-003-pentest-hardware.md) | Penetration Testing Hardware / Tool Usage | Document authorized hardware engagements and tool usage |

## Document control
Each form carries an ID, version, and status in its header so it can be referenced
and updated as a controlled document. New forms and procedures are registered in
SOP-001 as they are created.

## Status
Active and expanding as the program progresses. Planned additions include an
interactive CLI script (newwriteup.sh) for deploying forms quickly, and further
forms as the scope grows.
