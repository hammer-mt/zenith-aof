# Agency of the Future — Demo Run of Show

**Client:** Greenfield Bank (fictional challenger bank targeting millennials/Gen Z)  
**Total Runtime:** 25-30 minutes  
**Theme:** Every task synthesizes 3+ chaotic sources into one actionable view

---

## Pre-Demo Setup (Do This Before the Session)

```bash
# Clone or navigate to this repo
cd agency-demo

# Open 3-4 terminal windows/tabs for parallel Claude instances
# Label them: MAIN, AGENT-2, AGENT-3, AGENT-4
```

---

## Demo Flow

### Opening (Before Demo Starts)
"What I'm about to show you is how I'd actually structure an agency today. Every workflow is a reusable 'skill' that AI agents execute. Watch how many sources we synthesize — this is the opposite of 'draft me an email.'"

---

## DEMO 1: Report Commentary (5-6 min)
**Find performance insights from chaos**

### The Setup (Say This)
"Every week, planners spend hours writing performance commentary. They pull data from 4 different sources, compare to last week, check against client goals, look at benchmarks — then write 'impressions were up 12%.' Let's see what that looks like when AI does it."

### Run This
```bash
cd agency-demo
cat prompts/01-report-commentary.md | claude
```

### Sources Being Synthesized
1. `data/report-commentary/performance-week12.csv` — This week's platform data
2. `data/report-commentary/performance-week11.csv` — Last week for comparison
3. `data/report-commentary/client-goals.md` — Q1 KPIs and targets
4. `data/report-commentary/competitive-benchmarks.md` — Industry CPCs, CTRs
5. `data/report-commentary/last-week-commentary.md` — Previous commentary for continuity

### What to Narrate
- "Watch it pull from 5 different sources — two weeks of data, client goals, benchmarks, last week's commentary"
- "This is 2-3 hours of planner work. We're about to do it in 2 minutes."
- "Notice it's flagging anomalies I might miss at 6pm on Friday"
- Point out: "I review and edit — I don't write from scratch. That's the NCO Gap."

---

## DEMO 2: Meeting Notes → Action (5-6 min)
**Capture client intent from chaos**

### The Setup (Say This)
"Client calls are gold mines of information buried in 45 minutes of rambling. What did they actually want? Did they just change the scope? Does this contradict what we agreed last month? Let's find out."

### Run This
```bash
cat prompts/02-meeting-notes.md | claude
```

### Sources Being Synthesized
1. `data/meeting-notes/call-transcript-mar20.md` — Raw messy transcript
2. `data/meeting-notes/original-sow.md` — What we actually agreed to
3. `data/meeting-notes/campaign-status.md` — Where things stand now
4. `data/meeting-notes/previous-actions.md` — What we said we'd do last time

### What to Narrate
- "This transcript is messy — interruptions, tangents, someone's dog barking"
- "Watch it cross-reference against the SOW — did the client just ask for something out of scope?"
- "It's not just summarizing — it's flagging contradictions and scope creep"
- "The output is: here's what changed, here's what we owe, here's what needs escalation"

---

## DEMO 3 + 4: PARALLEL AGENTS (8-10 min)
**🔥 This is the "blow their minds" moment — run two agents simultaneously**

### The Setup (Say This)
"Now watch what Stage 6 looks like. I'm going to run two agents in parallel — one building a creative brief from competitor analysis, one running campaign simulation. Same time, different tasks."

### In Terminal 1 (AGENT-2): Creative Brief
```bash
cat prompts/03-creative-brief.md | claude
```

### In Terminal 2 (AGENT-3): Campaign Simulation
```bash
cat prompts/04-campaign-simulation.md | claude
```

### Sources Being Synthesized — Creative Brief
1. `data/creative-brief/competitor-ads.md` — 3 competitors' actual ad copy/positioning
2. `data/creative-brief/brand-guidelines.md` — Greenfield's voice, do's and don'ts
3. `data/creative-brief/audience-research.md` — Persona deep-dives
4. `data/creative-brief/historical-winners.csv` — What's worked before

### Sources Being Synthesized — Campaign Simulation
1. `data/campaign-simulation/creative-concepts.md` — 4 headline/copy options to test
2. `data/campaign-simulation/personas/` — 3 different audience personas
3. `data/campaign-simulation/historical-performance.md` — Past campaign results
4. `data/campaign-simulation/competitor-positioning.md` — What they're saying

### What to Narrate
- "Two agents, running simultaneously. This is Stage 6 — parallel YOLO mode."
- "The creative brief is analyzing 3 competitors plus our brand guidelines plus what's worked before"
- "The simulation is testing 4 concepts against 3 different personas"
- "Watch them both finish — neither waited for the other"
- When Campaign Simulation finishes: "This is the SIMULATE side of the Creative Testing Loop. We just de-risked 4 concepts before spending a dollar."

---

## DEMO 5: Vendor Monitoring (4-5 min)
**Audit work quality from chaos**

### The Setup (Say This)
"Vendors send us wrap reports — 40 pages of self-congratulation. Did they actually deliver what we paid for? Let's find out."

### Run This
```bash
cat prompts/05-vendor-monitoring.md | claude
```

### Sources Being Synthesized
1. `data/vendor-monitoring/vendor-wrap-report.md` — Their 40-page deck (condensed)
2. `data/vendor-monitoring/original-io.md` — What we actually bought
3. `data/vendor-monitoring/qa-checklist.md` — Our internal standards
4. `data/vendor-monitoring/platform-actuals.csv` — What the platforms actually reported

### What to Narrate
- "The vendor says they crushed it. But watch what happens when we cross-reference against the IO..."
- "It's flagging: they promised 2M impressions, delivered 1.6M. They said $8 CPM, actuals show $11."
- "This isn't just summary — it's audit. It knows what questions to ask."
- "This is managing by exception. I don't read 40 pages. I review the exceptions."

---

## Closing (After Demo)

"Every one of these tasks used to be 1-4 hours of work. We just did all five in under 30 minutes — with two running simultaneously. And I was reviewing, not doing. That's what 'everyone is a manager' actually looks like."

**Key callbacks:**
- "Report Commentary: NCO Gap — AI flags, I decide"
- "Meeting Notes: Synthesizing chaos into action"
- "Creative Brief + Simulation: Stage 6, parallel agents"
- "Vendor Monitoring: Managing by exception"
- "All five: New Taylorism — I could A/B test every one of these prompts"

---

## If Something Goes Wrong

**Claude hangs or errors:**
- "This is the NCO Gap in action — when it fails, I step in. Let me try a different approach."
- Switch to a backup: manually show one of the output files in `outputs/`

**It produces something weird:**
- "Notice I'm reviewing the output, not shipping it blind. This is why humans stay in the loop."

**Questions about cost/tokens:**
- "This entire demo cost maybe $2-3 in API calls. That's the trade-off — you're buying back hours of human time for pennies."

---

## Files Checklist

Before demo, confirm these exist:
- [ ] `prompts/01-report-commentary.md`
- [ ] `prompts/02-meeting-notes.md`
- [ ] `prompts/03-creative-brief.md`
- [ ] `prompts/04-campaign-simulation.md`
- [ ] `prompts/05-vendor-monitoring.md`
- [ ] All files in `data/` subdirectories
- [ ] Empty `outputs/` directory for Claude to write to
