# Reflection — From Study Notes to a Standard Operating Procedure

*Written within the first days of hands-on work in my self-directed cybersecurity program.*

When I started documenting my lab work, I wrote it the way a student takes notes — for myself, to remember what I did. A few days in, working through the OverTheWire Bandit levels, I noticed my write-ups changing shape on their own, and I followed that thread. This is a short record of how the approach evolved, because the evolution itself taught me something about how security work is actually done.

## The shift
I realized my write-ups read better structured like a technical/incident report than like personal notes — leading with an objective, describing the environment, walking through the actions taken and the reasoning behind them, and ending with a result and a takeaway. That mirrors how a SOC analyst documents an incident: the goal isn't to remember it yourself, it's to communicate it clearly to a team.

## From format to template
Once I'd settled on that structure, I noticed I was copying an older write-up each time to reuse the skeleton — and occasionally leaving stale details behind. The fix was to build a reusable template so every write-up starts consistent and correct.

## From template to controlled form
Then it clicked that a template like this isn't just a convenience — it's a form. Security teams work from standardized, versioned, referenceable documents. So I gave it a document-control header and an ID (FORM-001), the way a controlled document carries one.

## From a form to an SOP handbook
Once there was a FORM-001, the larger idea followed: a collection of standardized forms plus the procedures for using them is a Standard Operating Procedure (SOP) handbook — how teams keep documentation consistent, auditable, and repeatable across people. So I started building one, beginning with this first form.

## Why this matters
What I took from this is that security isn't only about solving the technical problem in front of you — it's about documenting it to a standard so the work is repeatable and communicable. Recognizing that, and building the structure for it early and on my own initiative, felt like a shift from "learning the tools" toward "thinking like the role."

## Repository progress
This portfolio has grown quickly alongside the learning: a documented study plan, structured Security+ notes, technical Bandit write-ups (with a visible progression from learning notes to incident-report format), a reusable write-up template (FORM-001), a small automation script that deploys it, and this reflection — the beginning of an SOP handbook.
