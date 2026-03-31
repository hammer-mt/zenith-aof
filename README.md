# Agency of the Future — Demo Run of Show

**Total Time:** 30-40 minutes  
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
- Previous simulation predictions vs. actual results (backtesting data)

**Run:**
```bash
cd data/04-campaign-simulation
cat ../prompts/04-campaign-simulation.md | claude
```

**Narrate while it runs:**
- "This is the SIMULATE side of the Creative Testing Loop."
- "It's not just rating headlines. It's simulating how each persona responds, why, and predicting which will perform."
- "But here's what closes the loop — it's also reading how accurate our LAST simulation was. Where we over-predicted, where we got it wrong."
- "Watch it recalibrate the personas based on real-world results. That's backtesting — the dashed line on the diagram."

**When done:** 
- "Look at the recalibration table — it adjusted Rachel's scores because last time we over-indexed on her rational side and missed her social drivers."
- "This isn't a one-shot prediction. It's a system that gets smarter every campaign. That's the closed loop."
- "We go to market with 2 concepts instead of 4, and our predictions are more accurate than last quarter's."

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

### Phase 6: Skill Improvement — The Real Job (5-6 min)

**🔥 This is the New Taylorism punchline — your job is improving the system, not doing the work.**

**Say:** "We've run 5 workflows. Now I'm going to show you what your actual job looks like in the agency of the future. It's not writing reports. It's not even reviewing reports. It's making the system that writes reports better."

**Run:**
```bash
cd data/06-skill-improvement
cat ../prompts/06-skill-improvement.md | claude
```

**Narrate while it runs:**
- "I'm feeding it the prompt we used for Report Commentary, the output it produced, and the raw data."
- "It's not redoing the report. It's auditing the skill — scoring the output, finding the highest-impact improvement."
- "This is what New Taylorism actually means: you A/B test and improve the prompts, not the deliverables."

**When done:**
- Read the suggested edit out loud — "It found [X weakness] and proposed a specific fix."
- **Make the edit live.** Open `prompts/01-report-commentary.md` in your editor, apply the change the agent suggested. (This should take 30 seconds.)
- **Re-run Report Commentary:**
  ```bash
  cd ../01-report-commentary
  cat ../prompts/01-report-commentary.md | claude
  ```
- Compare: "The output is now [better in the specific way the agent predicted]. One small edit to the skill, every future run improves."

**Land it:**
- "In a traditional agency, you'd train a junior for 6 months. Here, you improve a prompt in 30 seconds and every agent gets the upgrade instantly."
- "That's the job. You're not a doer. You're not even just a reviewer. You're a system builder."

---

### Phase 7: The Orchestrator Glimpse (2-3 min)

**Say:** "What you just saw was Stage 6 — me manually running multiple agents and improving them. Stage 8 is when you automate the orchestration itself."

**Show:** `orchestrator-example.md` — "This is what it looks like when you build your own loop. The agent runs continuously, checks for new data, runs the right workflow, flags exceptions for human review."

**Say:** "This is where it's going. You come in, review the exceptions, improve the skills, and the system runs 24/7."

---

### Phase 8: Close (2 min)

**Say:** 
- "Everything I showed you synthesized multiple chaotic sources into one actionable view."
- "The AI did the synthesis. I did the judgment."
- "And in the last step, I improved the system itself. That's the real leverage."
- "That's the NCO Gap. That's New Taylorism. That's the agency of the future."

**Ask:** "Which of these would save you the most time this week?"

---

## Troubleshooting

**If Claude gets stuck:** Kill it, restart with a simpler prompt, narrate "This is the reality — sometimes you have to course-correct. That's why you're the manager."

**If it's taking too long:** "Let's let that run and look at a pre-generated output" — have backup outputs in `outputs/` folder.

**If someone asks about cost:** "These 6 tasks cost about $4-6 total in API. A junior doing this manually is $50/hr for 4 hours. You do the math."

---

## Files Checklist

- [ ] `data/01-report-commentary/` — performance CSVs, goals, benchmarks, last week's notes
- [ ] `data/02-meeting-notes/` — transcript, previous notes, project scope, action items
- [ ] `data/03-creative-brief/` — competitor ads, brand guidelines, audience research, past performance
- [ ] `data/04-campaign-simulation/` — concepts, personas, historical data, client feedback
- [ ] `data/05-vendor-monitoring/` — wrap report, SOW, QA checklist, invoice
- [ ] `data/06-skill-improvement/` — copy of report commentary prompt + its output for review
- [ ] `prompts/` — all 6 prompt files
- [ ] `outputs/` — backup pre-generated outputs (in case of demo gremlins)
