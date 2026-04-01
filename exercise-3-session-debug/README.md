# Exercise 3: Debug the Session — Find the Skill Gaps

**Format:** Review a real AI session log (CSV) from the Exercise 1 live demo  
**Total Time:** 20-30 minutes  
**Your Role:** You're the manager reviewing how the AI performed. Find where it struggled, wasted time, or missed something — then propose a skill that would fix it.

---

## The Setup

In Exercise 1, we ran a live demo where Claude orchestrated 6 workflows for a fictional client (Lumina Skin). That entire session was logged.

We've converted that log from its raw JSON format into two CSVs that anyone can open in Excel or Google Sheets:

| File | What It Is |
|------|-----------|
| `data/session-log.csv` | 101 raw steps — every tool call, every file read, every AI output, every tool result, unedited |
| `data/session-summary.csv` | High-level stats: timing, cost, files read, phase breakdown |

---

## How to Read the Session Log

Open `data/session-log.csv`. Each row is one action. The columns are:

| Column | What It Means |
|--------|--------------|
| **Step** | Order of actions (1, 2, 3...) |
| **Timestamp** | When it happened |
| **Demo Phase** | Which demo was running (Report Commentary, Vendor Monitoring, etc.) |
| **Who** | "AI" or "Instructor" — who did this step |
| **Action Type** | What kind of action (Read, Bash, Agent, Text Output, Tool Result, AskUserQuestion, Thinking) |
| **Raw Content** | The actual unedited content — full file paths, full AI text output, full tool results |

---

## The Exercise

### Step 1: Explore the Data (5 min)

Open both CSVs. Scan through them. Notice:
- How many files did the AI read per demo?
- Where are the long gaps between timestamps?
- Which phases took the most time?
- What pattern do you see in how the AI works? (hint: read → read → read → produce)

### Step 2: Spot the Gaps (10 min)

Look for these types of issues:

**Efficiency gaps:** Where did the AI do unnecessary work? Where could it have been faster?

**Quality gaps:** Where did the AI probably miss something in the output? (You can cross-reference with the actual data files in `exercise-1-live-demo/data/`)

**Process gaps:** Where did the AI follow a pattern that a skill could standardize?

**Missing connections:** Did the AI connect insights across demos, or did it treat each one in isolation?

### Step 3: Write Your Skill Proposal (10 min)

Pick the ONE improvement that would have the biggest impact. Write a brief proposal:

1. **What's the gap?** (1-2 sentences)
2. **Which demo(s) does it affect?**
3. **What would the skill do?** (3-5 bullet points)
4. **How would you know it's working?** (what would the output look like differently)

---

## Things to Look For

Here are some starter questions to guide your analysis:

- The AI read 24 files across the session. Were all of them necessary? Could some have been skipped or combined?
- Two sub-agents ran in parallel for Demos 2+3. Could more demos have been parallelized?
- The AI paused 6 times for instructor input. Is that the right cadence for a live demo?
- Demo 6 (Skill Improvement) shows the AI going back to re-read files from Demo 1. Why? Could a skill have kept that context available?
- The session summary shows timing per phase. Which phases were fastest? Why? What made them efficient?

---

## Bonus: Compare to the Original JSON

The raw session data came from Langfuse (an AI observability tool) as JSON. The original file is at `data/original-session.json`. Compare the two formats:

- Which is easier to scan for patterns?
- Which gives you more detail?
- If you were reviewing 50 sessions (not just 1), which format would you want?

This is the meta-lesson: **the format of your data determines what insights you can find.** A CSV lets anyone — not just developers — spot the patterns.
