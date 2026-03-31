# Lumina Skin — Previous Simulation Predictions vs. Actuals
## Backtesting Reference for Persona Calibration

---

## Valentine's Day 2026 — Simulation vs. Reality

The simulation was run before the Valentine's campaign launched. Here's how the predictions compared to actual results.

### Concept-Level Predictions

| Concept | Predicted ROAS | Actual ROAS | Delta | Prediction Accuracy |
|---------|---------------|-------------|-------|---------------------|
| "Galentine's Glow" (friend gifting) | 2.6x | 3.4x | +0.8x | Under-predicted ❌ |
| "Love Your Skin" (self-purchase) | 3.0x | 2.5x | -0.5x | Over-predicted ❌ |
| "The Perfect Match" (partner gift) | 3.2x | 2.1x | -1.1x | Significantly over-predicted ❌ |
| "You Deserve This" (treat yourself) | 2.8x | 3.0x | +0.2x | Close ✅ |

### Persona-Level Prediction Accuracy

**Rachel (Sophisticate):**
- Predicted: Would respond best to "Love Your Skin" — clinical angle
- Actual: Highest engagement with "Galentine's Glow" — shared it with friends
- **Calibration note:** Rachel's social/community side was underweighted. She doesn't just buy for herself — she curates for her circle.

**Maya (Routine Seeker):**
- Predicted: Would respond best to "Galentine's Glow" — friend/community angle
- Actual: Confirmed — highest CTR and conversion from Maya segment
- **Calibration note:** Maya predictions were accurate. Her FOMO and community drivers are well-modeled.

**Diane (Results-Driven):**
- Predicted: Would respond best to "Love Your Skin" — self-care permission
- Actual: Responded to "You Deserve This" — more direct permission messaging
- **Calibration note:** Diane needs more explicit permission language, not clinical framing. "You deserve" > "Love your skin." She's past the education stage.

**James (Gift-Giver):**
- Predicted: Would respond best to "The Perfect Match" — gift positioning
- Actual: Very low engagement — Valentine's skincare from partner felt too personal/risky
- **Calibration note:** James's gift-giving confidence varies by occasion. He's confident buying skincare for Mother's Day (safe, appreciated) but not Valentine's Day (risky, might imply something). Occasion context matters more than we modeled.

---

## Holiday 2025 — Simulation vs. Reality (Partial Backtest)

Only 2 concepts were pre-simulated. Accuracy was better for this occasion.

| Concept | Predicted ROAS | Actual ROAS | Delta |
|---------|---------------|-------------|-------|
| "Gift of Glow" Set | 4.8x | 5.2x | +0.4x |
| "The Only Gift She Wants" | 4.0x | 4.3x | +0.3x |

**Notes:**
- Holiday gift-giving is a clearer occasion — personas behave more predictably
- Gift-giver personas (James-type) were accurately modeled for holiday
- Self-purchase personas were slightly under-predicted (Diane-types treat themselves more during holidays than expected)

---

## Known Biases in Current Persona Model

Based on backtesting across 3 campaigns:

1. **Over-indexes on rational/clinical drivers for Rachel and Diane.** Both have stronger social and emotional purchase triggers than the personas suggest.
2. **Under-indexes James's occasion sensitivity.** He's not a generic gift-giver — his confidence and behavior change dramatically by occasion.
3. **Maya is the most accurately modeled persona.** Her FOMO/community drivers are consistent across occasions.
4. **Self-purchase ROAS is systematically over-predicted** by ~0.3-0.5x. The personas are modeled as more self-motivated than they actually are.
5. **Friend-to-friend gifting is systematically under-predicted.** This is a blind spot — none of our personas explicitly model the "I'm buying this for my friend" behavior.

---

*Last backtest: March 2026*
*Covers: Holiday 2025, Valentine's 2026*
*Next backtest due after: Mother's Day 2026*
