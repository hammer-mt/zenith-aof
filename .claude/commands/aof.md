# Agency of the Future — Live Demo

You are orchestrating a live demo. The instructor is presenting to an audience and the terminal is projected on screen. Your output IS the demo.

## Rules

1. **Pause between every phase.** Use AskUserQuestion to ask "Ready for the next phase?" before continuing. Never auto-advance.
2. **Show talking points BEFORE doing work.** Display them as a blockquote so the instructor can read them to the audience while you prepare.
3. **Do the actual work inline** for most phases — the audience needs to see you reading files and producing output in real-time. The streaming output is the wow factor.
4. **Phase 3 is the exception** — dispatch two Agent subagents in parallel to demonstrate multi-agent orchestration. The audience sees both spinners running at once.
5. **Use clear headers and formatting.** The audience is reading your terminal from across a room.
6. **After each output, show teachable moments** as a highlighted block the instructor can riff on.
7. **If something goes wrong**, say: "This is the reality of working with AI — sometimes you course-correct. That's why you're the manager." Then move on.
8. **All exercise-1 files are under `exercise-1-live-demo/`.** Prompts are at `exercise-1-live-demo/prompts/`, data at `exercise-1-live-demo/data/`, outputs at `exercise-1-live-demo/outputs/`.

## Phase 1: Set the Stage

Display this to the audience:

---

# Agency of the Future

**Client:** Lumina Skin (fictional DTC skincare brand)

**What you're about to see:** 6 AI workflows that each synthesize 3-6 chaotic data sources into one actionable deliverable. At one point, two agents will run in parallel.

**The philosophy:** The AI does the synthesis. The human does the judgment.

---

Then run `ls exercise-1-live-demo/data/` via the Bash tool to show the folder structure.

After showing the folders, display:

> **6 folders of chaos.** Performance CSVs, messy transcripts, vendor invoices, competitor intel, brand guidelines. Sound familiar? Let's see what happens when AI agents tackle this.

Then ask the instructor if they're ready to start Demo 1 using AskUserQuestion.

---

## Phase 2: Report Commentary — Find Performance Insights

### Before the work

Display:

> **TALKING POINTS — Report Commentary**
> - "Every week, planners spend 2-3 hours pulling from 4+ sources to write performance commentary"
> - "Watch it cross-reference 6 files: three platforms of data, client goals, benchmarks, and last week's notes"
> - "This is the NCO Gap — it synthesizes, I review whether the strategic recs make sense"

### Do the work

1. Read `exercise-1-live-demo/prompts/01-report-commentary.md` to understand the task
2. Read ALL 6 files in `exercise-1-live-demo/data/01-report-commentary/`
3. Follow the prompt's instructions exactly — produce the full weekly commentary output
4. Format it clearly with headers so the audience can follow

### After the output

Display:

> **TEACHABLE MOMENT**
> - That was 6 sources synthesized into one commentary — ~2 minutes vs. 2-3 hours
> - It flagged anomalies, compared to benchmarks, checked progress against goals
> - "I'd review and tweak a few things — but I didn't write from scratch. That's the NCO Gap."

Then ask if the instructor is ready for Demos 2+3 (parallel) using AskUserQuestion.

---

## Phase 3: Meeting Notes + Creative Brief — PARALLEL

### Before the work

Display:

> **TALKING POINTS — Parallel Agents**
> - "Now watch: two completely different tasks running at the same time"
> - "Meeting notes is cross-referencing a messy transcript against the SOW, previous meeting, and open actions"
> - "Creative brief is analyzing 3 competitors plus brand guidelines plus historical performance"
> - "A human does these sequentially. We're doing them simultaneously."

### Do the work — DISPATCH TWO AGENTS SIMULTANEOUSLY

Use the Agent tool to launch BOTH of these in a single message (parallel tool calls):

**Agent 1 — Meeting Notes:**
Prompt the agent with:
"You are running a live demo. Read ALL of the following files, then follow the prompt instructions to produce the full meeting debrief output. Format it clearly with headers.

Prompt file: exercise-1-live-demo/prompts/02-meeting-notes.md
Data files (read ALL of these):
- exercise-1-live-demo/data/02-meeting-notes/meeting_transcript_march21.md
- exercise-1-live-demo/data/02-meeting-notes/previous_meeting_march14.md
- exercise-1-live-demo/data/02-meeting-notes/project_scope.md
- exercise-1-live-demo/data/02-meeting-notes/open_action_items.md

Read the prompt file first to understand the task structure, then read all data files, then produce the complete output as specified in the prompt."

**Agent 2 — Creative Brief:**
Prompt the agent with:
"You are running a live demo. Read ALL of the following files, then follow the prompt instructions to produce the full creative brief output. Format it clearly with headers.

Prompt file: exercise-1-live-demo/prompts/03-creative-brief.md
Data files (read ALL of these):
- exercise-1-live-demo/data/03-creative-brief/competitor_ads.md
- exercise-1-live-demo/data/03-creative-brief/brand_guidelines.md
- exercise-1-live-demo/data/03-creative-brief/audience_research.md
- exercise-1-live-demo/data/03-creative-brief/past_creative_performance.md

Read the prompt file first to understand the task structure, then read all data files, then produce the complete output as specified in the prompt."

### After both agents complete

Display BOTH outputs with clear separators, then:

> **TEACHABLE MOMENT**
> - Two tasks that would take 3-4 hours total, done simultaneously
> - Meeting notes flagged scope changes and contradictions. Creative brief found competitive white space.
> - "Both done. I'll spend 3 minutes reviewing instead of 2 hours creating."

Then ask if the instructor is ready for Demo 4 using AskUserQuestion.

---

## Phase 4: Campaign Simulation — De-Risk with Backtesting

### Before the work

Display:

> **TALKING POINTS — Campaign Simulation**
> - "This is the SIMULATE side of the Creative Testing Loop from the slides"
> - "It's testing 4 concepts against calibrated personas — Rachel, Maya, Diane, James"
> - "But here's the key: it's ALSO reading how accurate our LAST predictions were"
> - "Watch it recalibrate based on real-world results — that's the backtesting loop, the dashed line on the diagram"

### Do the work

1. Read `exercise-1-live-demo/prompts/04-campaign-simulation.md`
2. Read ALL 5 files in `exercise-1-live-demo/data/04-campaign-simulation/` (including `previous_simulation_predictions.md`)
3. Follow the prompt exactly — produce the full simulation report WITH the Persona Recalibration Report

### After the output

Display:

> **TEACHABLE MOMENT**
> - Point out the Persona Recalibration Report — "It adjusted for known biases from past campaigns"
> - "Last time we over-predicted self-purchase ROAS by 0.3-0.5x. This time it corrected for that."
> - "This isn't a one-shot prediction. It's a system that gets smarter every campaign. That's the closed loop."
> - "We go to market with 2 concepts instead of 4 — de-risked before spending a dollar."

Then ask if the instructor is ready for Demo 5 using AskUserQuestion.

---

## Phase 5: Vendor Monitoring — Audit Work Quality

### Before the work

Display:

> **TALKING POINTS — Vendor Monitoring**
> - "Vendors send us 40-page wrap reports full of self-congratulation"
> - "Did they actually deliver what we paid for? Does the invoice match the contract?"
> - "This is managing by exception — I don't read 40 pages, I review what the agent flags"

### Do the work

1. Read `exercise-1-live-demo/prompts/05-vendor-monitoring.md`
2. Read ALL 4 files in `exercise-1-live-demo/data/05-vendor-monitoring/`
3. Follow the prompt exactly — produce the full vendor audit report

### After the output

Display:

> **TEACHABLE MOMENT**
> - Point out the specific discrepancies: impressions delivered vs. promised, CPM variance, compliance gaps
> - "The vendor says they crushed it. The data says otherwise."
> - "NCO Gap: the agent did the forensics. I decide whether to push back or renegotiate."

Then ask if the instructor is ready for Demo 6: Skill Improvement using AskUserQuestion. Tease it: "This next one is the punchline — it's what your job ACTUALLY looks like in the agency of the future."

---

## Phase 6: Skill Improvement — The Real Job

### Before the work

Display:

> **TALKING POINTS — Skill Improvement (New Taylorism)**
> - "We've run 5 workflows. Now I'm going to show you what your actual job looks like."
> - "It's not writing reports. It's not even reviewing reports."
> - "It's improving the SYSTEM that writes reports. This is New Taylorism."

### Step 1: Run the skill improvement analysis

1. Read `exercise-1-live-demo/prompts/06-skill-improvement.md`
2. Read `exercise-1-live-demo/data/06-skill-improvement/skill_under_review.md` (the original report commentary prompt)
3. Read `exercise-1-live-demo/data/06-skill-improvement/skill_output.md` (the output it produced)
4. Also read a few key files from `exercise-1-live-demo/data/01-report-commentary/` to verify source utilization
5. Follow the prompt — produce the full improvement analysis: scoring, the suggested edit (with exact BEFORE/AFTER), and the impact prediction

### After the analysis

Display:

> **TEACHABLE MOMENT**
> - "It scored the output, found the single highest-impact improvement, and wrote the exact edit"
> - Read the BEFORE/AFTER aloud — "This is a 30-second change"
> - "In a traditional agency, you'd train a junior for 6 months. Here, you improve a prompt."

Then ask the instructor using AskUserQuestion: "Should I apply the suggested edit and re-run Report Commentary to show the improvement?"

### Step 2: If they say yes

1. Apply the suggested edit to `exercise-1-live-demo/prompts/01-report-commentary.md` using the Edit tool
2. Display: "Edit applied. Re-running Report Commentary with the improved skill..."
3. Read the UPDATED prompt and all data files in `exercise-1-live-demo/data/01-report-commentary/`
4. Produce the improved commentary

### After the re-run

Display:

> **TEACHABLE MOMENT**
> - Compare to the first run: "Notice [specific improvement the edit caused]"
> - "One edit. 30 seconds. Every future run is better."
> - "That's the job. You're not a doer. You're not even just a reviewer. You're a system builder."

Then ask if the instructor is ready for the closing phases using AskUserQuestion.

---

## Phase 7: The Orchestrator Glimpse

Read and display the contents of `exercise-1-live-demo/orchestrator-example.md`. Don't summarize — show the full document so the audience can see the Monday Morning Orchestrator example.

Then display:

> **TALKING POINTS — The Orchestrator**
> - "What you just saw was me running agents manually and improving them. Stage 8 is when you automate the orchestration itself."
> - "The orchestrator runs overnight — checks for new data, runs the right workflow, flags exceptions"
> - "You come in at 9am, review the exceptions, improve the skills, and the system runs 24/7"

Then ask if the instructor is ready to close using AskUserQuestion.

---

## Phase 8: Close

Display:

---

# The Agency of the Future

Everything you saw today:

1. **Report Commentary** — 6 sources synthesized in 2 minutes (not 2 hours)
2. **Meeting Notes + Creative Brief** — Two agents running in parallel
3. **Campaign Simulation** — Predictions calibrated against real-world results
4. **Vendor Monitoring** — 40 pages audited by exception
5. **Skill Improvement** — The system itself got better in 30 seconds

**The AI did the synthesis. I did the judgment. And then I improved the system.**

That's the NCO Gap. That's New Taylorism. That's the agency of the future.

---

> **CLOSING QUESTION for the audience:** "Which of these would save you the most time this week?"

---

> **If asked about cost:** "This entire demo cost about $4-6 in API calls. A junior doing this manually is $50/hr for 4+ hours. You do the math."

---

Display: "Demo complete." and stop.
