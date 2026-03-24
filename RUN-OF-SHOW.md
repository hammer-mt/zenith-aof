# Agency of the Future — Demo Run of Show

**Total Time:** 25-30 minutes  
**Client:** Lumina Skin (fictional DTC skincare brand)  
**Demo Philosophy:** Every task synthesizes 3+ chaotic sources into one actionable view.

---

## Pre-Demo Setup

1. Open 3-4 terminal windows (for parallel Claude instances)
2. Navigate to this repo in each: `cd agency-demo`
3. Have the slides ready with the "Agency of the Future" menu visible
4. Test that Claude Code is working: `claude`

---

## Demo Flow

### Phase 1: Set the Stage (2 min)

**Say:** "I'm going to show you what it looks like to manage AI agents instead of doing the work yourself. We have a fictional client — Lumina Skin, a DTC skincare brand. I'm going to run 5 different workflows, and at points I'll be running multiple agents in parallel. Watch how I'm reviewing and deciding, not doing."

**Show:** The `data/` folder structure — "Here's the chaos. Multiple folders, different formats, scattered information. Sound familiar?"

---

### Phase 2: Report Commentary (5-6 min)

**The chaos:** 
- Performance data from 3 platforms (Meta, Google, TikTok)
- Last week's commentary 
- Client's quarterly goals
- Industry benchmarks

**Run:**
```bash
cd data/01-report-commentary
cat ../prompts/01-report-commentary.md | claude
```

**Narrate while it runs:**
- "Four different sources. A human spends 2 hours cross-referencing."
- "Watch it pull in the benchmarks, compare to goals, write in the client's preferred format."
- "This is the NCO Gap — it's synthesizing, but I'm going to review whether the strategic recommendations make sense."

**When done:** Quickly scan output. "I'd tweak that recommendation about TikTok, but 90% of this is ready to send."

---

### Phase 3: Meeting Notes + Creative Brief (6-7 min) — PARALLEL

**Say:** "Now I'm going to run two agents in parallel. This is Stage 6 — multi-agent. Watch."

**Terminal 1 — Meeting Notes:**
```bash
cd data/02-meeting-notes
cat ../prompts/02-meeting-notes.md | claude
```

**Terminal 2 — Creative Brief:**
```bash
cd data/03-creative-brief
cat ../prompts/03-creative-brief.md | claude
```

**Narrate while both run:**
- "Two completely different tasks running simultaneously."
- "Meeting notes is synthesizing: raw transcript, previous meeting, project scope, open action items."
- "Creative brief is synthesizing: competitor ads, brand guidelines, audience research, past performance."
- "A human does these sequentially. I'm doing them in parallel and reviewing both."

**When done:** Flip between outputs. "Both done. I'll spend 3 minutes reviewing instead of 2 hours creating."

---

### Phase 4: Campaign Simulation (6-7 min)

**The chaos:**
- 4 headline concepts from creative team
- 3 persona definitions
- Historical performance on similar concepts
- Client feedback themes from past campaigns

**Run:**
```bash
cd data/04-campaign-simulation
cat ../prompts/04-campaign-simulation.md | claude
```

**Narrate while it runs:**
- "This is the SIMULATE side of the Creative Testing Loop."
- "It's not just rating headlines. It's simulating how each persona responds, why, and predicting which will perform."
- "Notice it's pulling in the historical data — 'concepts like this performed X% better when...' "
- "This is the world model. If I run this concept, what happens?"

**When done:** 
- "Look — it predicted Concept B will resonate with Persona 2 but alienate Persona 3. That's the kind of insight you'd get from a $30K focus group."
- "We go to market with 2 concepts instead of 4. Already saved the client money."

---

### Phase 5: Vendor Monitoring (5-6 min)

**The chaos:**
- Vendor's wrap report (40 pages of data)
- Original SOW/brief
- QA checklist
- Invoice vs. actual deliverables

**Run:**
```bash
cd data/05-vendor-monitoring
cat ../prompts/05-vendor-monitoring.md | claude
```

**Narrate while it runs:**
- "This came directly from your survey — invoice reconciliation, QA, checking vendor work."
- "It's cross-referencing: did they deliver what the SOW promised? Does the invoice match? Any red flags?"
- "This is managing by exception. I'm not reading 40 pages. I'm reviewing what the agent flagged."

**When done:**
- Point out any discrepancies it found
- "NCO Gap — it flagged that the vendor billed for 50K impressions on a placement that delivered 42K. I decide whether to push back."

---

### Phase 6: The Orchestrator Glimpse (2-3 min)

**Say:** "What you just saw was Stage 6 — me manually running multiple agents. Stage 8 is when you automate the orchestration itself."

**Show:** `orchestrator-example.md` — "This is what it looks like when you build your own loop. The agent runs continuously, checks for new data, runs the right workflow, flags exceptions for human review."

**Say:** "This is where it's going. You come in, review the exceptions, make the judgment calls, and the system runs 24/7."

---

### Phase 7: Close (2 min)

**Say:** 
- "Everything I showed you synthesized multiple chaotic sources into one actionable view."
- "The AI did the synthesis. I did the judgment."
- "That's the NCO Gap. That's New Taylorism. That's the agency of the future."

**Ask:** "Which of these would save you the most time this week?"

---

## Troubleshooting

**If Claude gets stuck:** Kill it, restart with a simpler prompt, narrate "This is the reality — sometimes you have to course-correct. That's why you're the manager."

**If it's taking too long:** "Let's let that run and look at a pre-generated output" — have backup outputs in `outputs/` folder.

**If someone asks about cost:** "These 5 tasks cost about $3-5 total in API. A junior doing this manually is $50/hr for 4 hours. You do the math."

---

## Files Checklist

- [ ] `data/01-report-commentary/` — performance CSVs, goals, benchmarks, last week's notes
- [ ] `data/02-meeting-notes/` — transcript, previous notes, project scope, action items
- [ ] `data/03-creative-brief/` — competitor ads, brand guidelines, audience research, past performance
- [ ] `data/04-campaign-simulation/` — concepts, personas, historical data, client feedback
- [ ] `data/05-vendor-monitoring/` — wrap report, SOW, QA checklist, invoice
- [ ] `prompts/` — all 5 prompt files
- [ ] `outputs/` — backup pre-generated outputs (in case of demo gremlins)
