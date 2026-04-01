# Agency of the Future — Workshop

Three exercises for the Zenith/RebelLion cohort.

---

## Exercise 1: Live Demo — AI Workflows in Action

**Time:** 30-40 min  
**Format:** Instructor-led demo with 6 AI workflows running live on a fictional client (Lumina Skin)  
**Key concepts:** NCO Gap, New Taylorism, multi-agent orchestration, skill improvement loops

See [exercise-1-live-demo/README.md](exercise-1-live-demo/README.md) for the full run of show.

**To run:**
```bash
claude /aof
```

---

## Exercise 2: Deep-Dive — Make It Agent-Native

**Time:** 30-40 min  
**Format:** 6 participants present their real workflow ideas (~5 min each). Instructor reframes each through the agent-native lens.  
**Key concepts:** What the AI synthesizes, what the human judges, what the v1 looks like

See [exercise-2-deep-dive/README.md](exercise-2-deep-dive/README.md) for all 6 submitted ideas with prep notes.

---

## Submitted Ideas (Exercise 2)

| # | Idea | Quick Take |
|---|------|-----------|
| 1 | WBS & project planning | Template-based, good first agent |
| 2 | Data standardization (MDI) | Mapping/rosetta stone pattern |
| 3 | Budget QA across systems | Narrowest scope — quick win |
| 4 | Billing & invoice reconciliation | Most complex, multi-team chain |
| 5 | Campaign reporting (end-to-end) | Best-written submission, strongest example |
| 6 | Vendor wrap report summaries | Direct connection to Exercise 1 Demo 5 |

---

## Exercise 3: Debug the Session — Find the Skill Gaps

**Time:** 20-30 min  
**Format:** Participants review the actual session log from the Exercise 1 demo (converted to CSV). Find where the AI struggled or missed something, then propose a skill improvement.  
**Key concepts:** Observability, session debugging, identifying skill gaps from logs, data format accessibility

See [exercise-3-session-debug/README.md](exercise-3-session-debug/README.md) for the full exercise.

**Data files:**
- `data/session-log.csv` — 101 raw steps from the live demo, readable in Excel/Sheets
- `data/session-summary.csv` — high-level stats and phase timing
- `data/original-session.json` — raw Langfuse export for comparison
