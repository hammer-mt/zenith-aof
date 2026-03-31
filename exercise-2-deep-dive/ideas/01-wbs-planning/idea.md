# Idea 1: Automated WBS Development & Project Planning

## What They Said

> Streamline WBS development & project planning from manual to automated.
>
> A structured workflow document that outlines both high-level and detailed task processes. It functions as a checklist specifying the actions required, the responsible individuals, and the stage at which each task should occur, clearly defining roles and responsibilities throughout the process.

## Current Pain

- WBS (Work Breakdown Structure) creation is manual and repetitive
- Each project requires defining tasks, owners, sequencing, and dependencies
- Lots of institutional knowledge about "what usually happens" locked in people's heads
- New projects copy-paste from old ones, but drift from the template

## Agent-Native Reframe

**AI synthesizes:** Past project WBS documents + project brief + team roster + known dependencies → draft WBS with task assignments, sequencing, and time estimates based on historical patterns.

**Human judges:** Whether the structure fits THIS project's nuances — unusual stakeholders, compressed timelines, new vendors, scope changes from the norm.

**System improvement loop:** After each project, compare the AI-generated WBS to what actually happened. Where did tasks get added, removed, or resequenced? Feed that back to improve future drafts.

**v1 this week:** Take 3-5 completed project WBS docs + a new project brief. Prompt: "Based on these past projects, generate a WBS for this new project. Flag where you're uncertain."
