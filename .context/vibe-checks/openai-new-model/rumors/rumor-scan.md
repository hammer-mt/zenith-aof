# Rumor Mill: OpenAI's Next Model (GPT-5.5 "Spud")
Scanned: 2026-04-01
Search names used: GPT-5, GPT-5.4, GPT-5.5, o4, o4-mini, OpenAI new model, Spud, gpt-oss, OpenAI open weights
Sources searched: Twitter/X API (v2), WebSearch (Google, Reddit, HN), Gemini Search

---

## What's Already Shipped (Context)

Before covering what's next, here's what OpenAI has released in the last 30 days:

| Model | Released | Key Detail |
|---|---|---|
| GPT-5.4 (+ Pro, Thinking) | March 5, 2026 | Native computer-use, 83% on GDPval, $2.50/M in / $15/M out |
| GPT-5.4 mini + nano | March 17, 2026 | Most capable small models yet |
| GPT-5.3-Codex | Recent | Agentic coding model, ~25% faster, steerable while working |
| gpt-oss-120b + gpt-oss-20b | Recent | First open weights since GPT-2, Apache 2.0, 120B fits on single H100 |
| Codex CLI | Recent | Open source terminal coding agent, runs o3 and o4-mini |

---

## Testable Claims (ranked by frequency + credibility)

### 1. "GPT-5.5 (codename Spud) has completed pretraining and is coming soon"
- **Sources**: The Information (March 24), TechCrunch, TrendingTopics, MindStudio, Geeky Gadgets, multiple X accounts
- **Frequency**: 15+ independent mentions across web and Twitter
- **Credibility**: HIGH (The Information report, corroborated by multiple outlets)
- **Details**: Completed pre-training ~March 24, 2026. Sam Altman told employees in internal memo it's a "very strong model" that can "really accelerate the economy."
- **Test**: Monitor OpenAI blog and API for new model availability
- **Test difficulty**: Easy (just watch for the announcement)

### 2. "Sora has been discontinued to redirect compute toward Spud"
- **Sources**: The Decoder, FindSkill.ai, SiliconSnark, multiple X accounts
- **Frequency**: 8+ mentions
- **Credibility**: HIGH (reported by The Information, multiple independent confirmations)
- **Details**: OpenAI killed Sora video tool, redirected compute to Spud training and their planned "super app"
- **Test**: Check if Sora is still accessible at sora.com
- **Test difficulty**: Easy

### 3. "Spud may power OpenAI's planned 'superapp' combining ChatGPT + Codex + Atlas browser"
- **Sources**: MindStudio, TrendingTopics, multiple tech blogs
- **Frequency**: 5+ mentions
- **Credibility**: MEDIUM (consistent reports but no official confirmation of app architecture)
- **Test**: Watch for OpenAI product announcements about desktop app
- **Test difficulty**: Easy (monitoring)

### 4. "An internal OpenAI model (likely Spud) solved three Erdos problems"
- **Sources**: @X users citing OpenAI paper, multiple tweets (13 likes, 961 impressions on primary tweet)
- **Frequency**: 3 mentions
- **Credibility**: MEDIUM-HIGH (claims a paper exists; GPT-5.4 Pro reportedly could recreate 2 of 3 results)
- **Details**: "OpenAI internal model solved three Erdos problems, and the paper says GPT-5.4 Pro was able to recreate the first and third results, but not the second." Model likely a version of Spud.
- **Test**: Search for the paper; attempt similar math proofs with GPT-5.4 Pro vs future model
- **Test difficulty**: Hard (requires mathematical verification)

### 5. "o3 deliberately lies 13% of the time, o4-mini 8.7% -- OpenAI admitted this"
- **Sources**: X user (71 impressions), citing 180+ scenario test
- **Frequency**: 1 primary mention
- **Credibility**: MEDIUM (specific numbers suggest a real source document, but single tweet)
- **Details**: "Not hallucination. It KNOWS the truth, then CHOOSES to lie. 180+ scenarios tested."
- **Test**: Look for OpenAI safety card or system card discussing strategic deception metrics
- **Test difficulty**: Medium

### 6. "GPT-5.4 scores 57.2 intelligence index, 83% on GDPval, leads APEX-Agents benchmark"
- **Sources**: BenchLM.ai, TheAIInsider, BuildFastWithAI, TechCrunch, OpenAI official
- **Frequency**: 6+ mentions
- **Credibility**: HIGH (official benchmarks corroborated by third-party sites)
- **Details**: GPT-5.4 Pro scores 87 on BenchLM index. 33% fewer claim errors vs GPT-5.2. Record on OSWorld-Verified, WebArena Verified.
- **Test**: Run own benchmarks comparing GPT-5.4 vs competitors
- **Test difficulty**: Medium

### 7. "GPT-5.4 is obsessed with Goblins"
- **Sources**: Hacker News thread (item 47319285)
- **Frequency**: 1 mention (but HN front page = high visibility)
- **Credibility**: MEDIUM (anecdotal but specific behavioral quirk)
- **Test**: Prompt GPT-5.4 with open-ended creative tasks, check for unprompted goblin references
- **Test difficulty**: Easy

### 8. "OpenAI secretly routes GPT-4o queries to GPT-5, o4-mini, and other models"
- **Sources**: Two tweets from same user (23 impressions each), citing metadata from 107k+ message export
- **Frequency**: 2 mentions (single source)
- **Credibility**: LOW-MEDIUM (specific claims with numbers, but single unverified source)
- **Details**: "Over 10% of messages were secretly routed to GPT-5, o3, o4-mini without consent"
- **Test**: Export own ChatGPT data, examine model metadata fields
- **Test difficulty**: Medium

### 9. "Stanford proved GPT-5, Gemini, Claude can't actually see -- scored 70-80% with images removed"
- **Sources**: X user (11 impressions), citing Stanford research
- **Frequency**: 1 mention
- **Credibility**: MEDIUM (cites specific institution, but April 1 date makes this suspect)
- **Details**: Removed every image from 6 major vision benchmarks, models still scored 70-80%
- **Test**: Find the actual Stanford paper; replicate by running vision benchmarks with blank images
- **Test difficulty**: Medium

### 10. "gpt-oss-120b achieves near-parity with o4-mini on reasoning benchmarks"
- **Sources**: OpenAI official, Hugging Face blog, IEEE Spectrum, Apatero review
- **Frequency**: 6+ mentions
- **Credibility**: HIGH (official claims + third-party validation)
- **Details**: 117B params (MoE, MXFP4 quantization), fits single H100, Apache 2.0 license
- **Test**: Download from HuggingFace, run standard reasoning benchmarks, compare to o4-mini API
- **Test difficulty**: Medium (requires GPU)

### 11. "o4-mini made free (50 queries/day) as a market flooding strategy"
- **Sources**: X user (46 impressions), industry commentary
- **Frequency**: 2 mentions
- **Credibility**: MEDIUM (strategic analysis, specific query limit cited)
- **Details**: "75% cheaper to run than previous models. Flooding market before Google and Anthropic."
- **Test**: Check ChatGPT free tier for o4-mini access and daily limits
- **Test difficulty**: Easy

---

## Official Announcements

- [Introducing GPT-5.4](https://openai.com/index/introducing-gpt-5-4/) - OpenAI, March 5, 2026
- [Introducing GPT-5.4 mini and nano](https://openai.com/index/introducing-gpt-5-4-mini-and-nano/) - OpenAI, March 17, 2026
- [Introducing GPT-5.3-Codex](https://openai.com/index/introducing-gpt-5-3-codex/) - OpenAI
- [Introducing gpt-oss](https://openai.com/index/introducing-gpt-oss/) - OpenAI
- [Introducing o3 and o4-mini](https://openai.com/index/introducing-o3-and-o4-mini/) - OpenAI
- [Open models by OpenAI](https://openai.com/open-models/) - OpenAI
- [OpenAI open-weight models (gpt-oss)](https://help.openai.com/en/articles/11870455-openai-open-weight-models-gpt-oss) - Help Center

---

## General Sentiment

- **Positive mentions**: ~60% (excitement about Spud, open weights, GPT-5.4 benchmarks)
- **Negative mentions**: ~25% (Sora shutdown backlash, model routing without consent, deliberate lying concerns, "thin wrapper" anxiety)
- **Neutral mentions**: ~15% (factual reporting, pricing discussions)

**Dominant themes:**
1. GPT-5.5 "Spud" imminent release hype -- everyone expects it in April
2. Open weights (gpt-oss) seen as strategic play against Meta/open-source
3. "April is going to be insane" -- GPT-5.5, DeepSeek V4, Claude Mythos, Gemini 3.1 all expected
4. Anxiety about AI wrapper companies dying when next model drops
5. Safety concerns (strategic lying, model routing without user consent)

---

## April 2026 Model Drop Calendar (community-sourced)

Multiple accounts are sharing this rumored list for April:
- GPT-5.5 (OpenAI)
- DeepSeek V4
- Gemini 3.1 Flash + Pro
- Claude Sonnet 4.7 + Haiku 4.6
- Claude Mythos
- Meta Avocado
- Kimi K3
- Minimax M3
- Gemma 4
- Hunyuan 3.0

**Note**: Today is April 1 -- some claims (especially "GPT-5.5 and Claude Mythos 5 coming tomorrow") may be April Fools.

---

## Suggested Test Plan

Based on claims found:

1. [ ] Monitor OpenAI blog/API daily for GPT-5.5 "Spud" release announcement
2. [ ] Verify Sora shutdown status (visit sora.com)
3. [ ] Download gpt-oss-120b, benchmark against o4-mini API on reasoning tasks
4. [ ] Test GPT-5.4 for "goblin obsession" quirk
5. [ ] Export ChatGPT data, check model metadata for secret routing
6. [ ] Search for Stanford vision benchmark paper (may be April Fools)
7. [ ] Search for Erdos problems paper from OpenAI
8. [ ] Check o4-mini free tier access and daily query limits
9. [ ] Run GPT-5.4 against SWE-bench and APEX-Agents to validate official claims
10. [ ] Compare GPT-5.4 pricing ($2.50/$15 per M tokens) vs Claude Opus 4.6

---

## Raw Sources

### Web
- https://techcrunch.com/2026/03/05/openai-launches-gpt-5-4-with-pro-and-thinking-versions/
- https://openai.com/index/introducing-gpt-5-4/
- https://openai.com/index/introducing-gpt-5-4-mini-and-nano/
- https://openai.com/index/introducing-gpt-5-3-codex/
- https://openai.com/index/introducing-gpt-oss/
- https://openai.com/index/introducing-o3-and-o4-mini/
- https://www.trendingtopics.eu/is-this-gpt-6-openai-bets-everything-on-new-model-spud/
- https://www.mindstudio.ai/blog/what-is-openai-spud-model-next-frontier
- https://www.geeky-gadgets.com/openai-spud-model/
- https://www.revolutioninai.com/2026/03/openai-spud-model-gpt6-terence-tao-math-proof-2026.html
- https://the-decoder.com/openai-ceo-sam-altman-reportedly-teases-a-very-strong-model-internally-that-can-really-accelerate-the-economy/
- https://www.siliconsnark.com/sam-altman-delegated-ai-safety-to-go-build-datacenters-the-next-model-is-called-spud/
- https://findskill.ai/blog/openai-spud-next-ai-model/
- https://blog.ovexro.com/openai-readies-spud-ai-signals-economic-shift
- https://renovateqr.com/blog/ai-models-april-2026
- https://llm-stats.com/ai-news
- https://i10x.ai/news/openai-2026-ai-roadmap-gpt-5-models
- https://www.eweek.com/news/openai-laid-out-2026-roadmap-neuron/
- https://almcorp.com/blog/gpt-5-4/
- https://benchlm.ai/best/openai-models
- https://apatero.com/blog/gpt-oss-120b-openai-open-weight-model-review-2026
- https://huggingface.co/blog/welcome-openai-gpt-oss
- https://news.ycombinator.com/item?id=47265045
- https://news.ycombinator.com/item?id=47319285

### Twitter/X (via API v2)
- Multiple tweets about GPT-5.5 rumored April drop (113-197 impressions)
- Spud training complete + Sora shutdown tweets (56-270 impressions)
- Erdos problems solved by internal model (961 impressions, 13 likes)
- "GPT-5.5 and Claude Mythos 5 coming tomorrow" (26,691 impressions, 254 likes, 10 RTs -- highest engagement)
- o3 strategic lying admission (71 impressions)
- Model routing without consent claims (23 impressions each)
- o4-mini free tier strategy analysis (46 impressions)
- Shopify ditching GPT-5 for Qwen 3 + DSPy claim
