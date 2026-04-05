## Simulation Spec: Bold Play vs. Timid Play in Negative-EV Games

---

### Problem Statement

Given a player with bankroll **B**, target **T**, and a game with edge **e** (negative), compare the probability of reaching T before ruin under different fixed bet sizes. Verify that bold play (largest allowable bet) dominates timid play when the goal is target-reaching, not survival.

---

### Mathematical Foundation (must be stated before any code runs)

**Gambler's Ruin closed form** (fair game):

> P(ruin | start=B, target=T, bet=k) = (T−B) / T

**Biased game** (edge e ≠ 0), let q/p = odds ratio:

> P(reach T) = (1 − (q/p)^(B/k)) / (1 − (q/p)^(T/k))

Sources the simulation must cite inline:
- Dubins & Savage, *How to Gamble If You Must* (1965) — bold play optimality theorem
- Feller, *An Introduction to Probability Theory* Vol. I, Ch. XIV — Gambler's Ruin derivation
- Ethier & Tavare (1983) for negative-EV generalization

---

### Simulation Architecture

**Two layers, both must run and agree:**

1. **Closed-form calculator** — computes exact P(reach T) from the biased Gambler's Ruin formula across a range of bet sizes
2. **Monte Carlo engine** — runs N=50,000 trials per bet size, tracking ruin vs. target outcomes

If the two layers disagree by >1%, the UI flags it explicitly rather than silently averaging.

---

### Parameters (all user-adjustable)

| Parameter | Default | Range |
|---|---|---|
| Starting bankroll B | £10M | £1k – £1B |
| Target T | £100M | > B |
| House edge e | −0.5% | −5% to −0.01% |
| Bet sizes to compare | £25k, £100k, £500k, £1M | Any set |
| Monte Carlo trials N | 50,000 | 1k – 500k |

---

### Reasoning Documentation Layer

Before each computational step, the UI renders a **reasoning block**:

```
[STEP 1 — Model selection]
Claim: Bold play maximizes P(reach T) in subfair games.
Source: Dubins & Savage (1965), Theorem 1.
Assumption: Bets are discrete, no fractional units, no table limits.
Proceeding to: closed-form calculation.
```

This is not post-hoc. The source and assumption must appear *before* the number, not after.

---

### Output Requirements

**Primary output:** Probability curve — P(reach T) vs. bet size k, plotted continuously, with Monte Carlo points overlaid as dots against the closed-form curve.

**Secondary outputs:**
- Expected number of bets before resolution (target or ruin), per bet size
- Median session length in time (if rounds/hour is set)
- A clearly labeled "crossover point" if one exists where timid play would ever be preferable (it won't for target-reaching, but the UI should prove this, not assert it)

**Sanity check panel** (always visible):
- Closed-form P vs. Monte Carlo P, per bet size
- Delta and pass/fail flag

---

### UI Behavior

- All parameters live-adjustable with instant recalculation
- Reasoning blocks collapsible but present by default
- Sources rendered as footnotes with full citations, not just author names
- No result is shown without its reasoning block having rendered first — enforce this in render order, not just visually

---

### Explicit Failure Mode Guard

The simulation must include a test case where the *intuitive* answer is wrong:

> **Preloaded scenario:** "Would you rather have 400 attempts at £25k or 100 attempts at £100k?"

Run both. Show that the £100k strategy wins on P(reach T) despite fewer attempts. Label this the **Dubins-Savage demonstration**.

---
