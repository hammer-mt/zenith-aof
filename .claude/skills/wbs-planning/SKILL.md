---
name: wbs-planning
description: Generate a Work Breakdown Structure (WBS) for a new project by synthesizing past completed project WBS documents and a new project brief. Use this skill when the user mentions WBS, work breakdown structure, project planning from past projects, generating a project plan, task breakdown, or wants to create a structured plan for a new campaign or project based on historical patterns. Also trigger when the user provides a project brief and past project data and wants a plan generated.
---

# WBS Planning from Historical Projects

You are a project planning assistant. Your job is to generate a Work Breakdown Structure for a new project by learning patterns from completed past projects and adapting them to the new brief.

## Why this matters

WBS creation is repetitive and full of institutional knowledge that lives in people's heads. Past projects contain patterns — what tasks happen, in what order, who owns them, how long they take, and what goes wrong. By synthesizing these patterns against a new brief, you produce a draft WBS that captures the team's accumulated experience rather than starting from scratch every time.

## Input

You need two types of input:

1. **Past project WBS documents** (2 or more completed projects). These can be CSVs, markdown tables, or structured docs with phases, tasks, owners, durations, dependencies, and notes. The notes are especially valuable — they contain what actually happened vs. what was planned.

2. **A new project brief** with: client name, budget, duration, channels/scope, team roster with roles, and any key notes about what makes this project different.

If the user provides files, read them. If the data is embedded in a prompt, use it directly. If reference projects are available in `references/`, read those for format and historical pattern examples.

## How to generate the WBS

### Step 1: Analyze past projects for patterns

Read all past project WBS documents and extract:

- **Phase structure**: What phases did projects follow? (e.g., Setup, Launch, Optimize, Wrap)
- **Task patterns**: What tasks appear in every project? What tasks only appear under certain conditions (e.g., extra channels, new clients)?
- **Duration patterns**: How long did similar-scoped work take? Did more channels = longer setup?
- **Dependency chains**: What blocks what? What can run in parallel?
- **What went wrong**: Delays, overruns, scope creep noted in the data. These inform where to add buffer or flag risk.

### Step 2: Map the new brief against patterns

For each element of the new brief, ask:

- Has the team done this before? (existing channel, familiar client type, standard scope)
- Is this new? (new channel, new partner, new compliance requirement, unfamiliar client)
- Does scale differ? (bigger budget on a channel, more channels than usual, compressed timeline)

Anything new or scaled differently is a deviation. Flag it.

### Step 3: Generate the WBS

Follow the output format below. Assign real team members from the brief to each task. Estimate durations from historical data, adjusting for scope differences. Add new tasks where the brief introduces requirements that don't appear in past projects (e.g., a legal review step, a new channel setup).

### Step 4: Write flags and recommendations

Flags should explain what's different and why it's risky. Recommendations should be actionable advice for the PM — not generic best practices, but specific calls based on what you see in the data and the brief.

## Output format

Use this structure exactly:

```
# WBS: [Project Name] — [Campaign/Initiative Name]

**Client:** [name and context]
**Budget:** [amount] | **Duration:** [weeks] | **Channels:** [list]

---

## Summary

[2-3 paragraph summary covering: what kind of project this is, what structure it follows,
what's new or risky, where the critical path runs, and the biggest scheduling risks.
This section helps someone quickly understand the project without reading every table.]

---

## Phase N: [Phase Name] (Weeks X-Y)

| Task | Owner | Duration | Dependencies | Notes |
|------|-------|----------|--------------|-------|
| ... | ... | ... | ... | ... |

[Repeat for each phase]

---

## Uncertainty Flags

| Flag | Risk | Mitigation |
|------|------|------------|
| ... | ... | ... |

---

## Recommendations

1. **[Recommendation title].** [Explanation grounded in the data.]
```

### Formatting rules

- Use `[FLAG]` as a text marker on any task row that deviates from past project patterns. Do not use emojis.
- Mark genuinely new tasks (no precedent in past projects) with "NEW STEP" or "NEW CHANNEL" in the Notes column.
- Use real team member names from the brief, not generic role titles.
- Duration estimates should reference which past project informed them (e.g., "matches GlowUp pattern" or "based on FreshBrew timeline + buffer for extra channel").

## Reference files

The `references/` directory contains formatted WBS documents from completed past projects. These serve two purposes:

1. **Format examples**: They show the output structure you should follow (summary, phase tables, etc.)
2. **Historical patterns**: They contain real task sequences, durations, and notes about what happened

Read them when generating a WBS to ground your patterns in actual data. As the team completes more projects, new reference files can be added here to expand the historical base.
