# HydroMind — StartSmart Prototype

Build material for the HydroMind three-screen coordination demo, produced for
**StartSmart / تحدي الجامعات 2026 — Jeddah Camp**.

**Team:** Amro Yousef (build + present) · Layan Turkistani (scenario, content, Arabic, verification + present)
Nawar Alimam and Tariq Tadmori are on the HydroMind capstone team but are not part of this build.

---

## What this is

A three-screen prototype that takes one realistic Mishkat Farm operating scenario and shows
the thing no competitor has: **two agents making individually correct requests that conflict
at the farm level, and an Orchestrator resolving them into one decision.**

```
Farm Status  →  Agent Analysis  →  HydroMind Decision
حالة المزرعة      تحليل الوكلاء        قرار HydroMind
```

Screen 2 is the hero. Screens 1 and 3 on their own would resemble products already on the
market; the visible conflict is the differentiation.

> Separate systems can make locally correct decisions that conflict at the farm level.
> HydroMind coordinates them into one system-level decision and explains why.

---

## Repository layout

| Path | What it is |
|---|---|
| `docs/HydroMind-Creative-Brief.md` | Strategy: product definition, hypothesis, scope, honesty rules, bilingual direction, roles |
| `docs/HydroMind-Storyboard.md` | Build spec: the scenario with its arithmetic, all three screens, agent messages, build order, acceptance checklist |
| `design/*.dc.html` | The four artboards — three screens plus a build-brief board |
| `design/canvas.json` | Canvas layout: artboard positions and sticky notes |
| `design/build/hydromind-prototype-screens.html` | The assembled canvas. Open it in a browser to view and export the screens. Generated — edit the artboards, not this file. |

---

## The scenario

Mishkat Farm, Jeddah. Four-zone NFT rig, shared 100 L reservoir, butterhead lettuce, hot
afternoon. A **realistic operating scenario built from the farm's operating ranges** — not a
recorded historical event.

| Variable | Reading | Target | Interpretation |
|---|---|---|---|
| pH | 6.42 ↗ | 5.5 – 6.5 | **In range** — monitor, no dose |
| EC | 2.41 mS/cm | 1.80 ± 0.10 | High → dilution request |
| Water level | 62 % (62.0 L) | 70 – 90 % | Low → refill request |
| Water temp | 24.6 °C | 18 – 22 °C | High → chiller |
| Mode | NORMAL | — | Coordination problem, not emergency |

Three readings are outside their operating targets. pH is not one of them.

**The conflict.** ReservoirAgent requests +28 L. ECController requests dilution equivalent to
≈ +21 L. Both are P2 Crop Health, both are correct, and both act on the same reservoir —
priority alone cannot separate them.

**The resolution.** Shared-resource merge: one 21 L action brings the level to 83 % (inside
the band) and EC to ≈ 1.80 (on target). Then process sequencing — chiller in parallel,
then mix, re-measure, and dose only if still required.

**Dilution estimate** (an approximation, not mass conservation; assumes temperature-compensated
EC and approximately linear dilution):

```
C₁V₁ ≈ C₂V₂
2.41 × 62 ≈ 1.80 × V₂
V₂ ≈ 83.0 L   →   fresh water ≈ 21.0 L
```

Float/overflow cutoff is 95 %, not 100 %.

---

## Honesty rules — non-negotiable

These exist because a judge will test them.

- Screen 1 always shows **SIMULATED FARM STATE / حالة مزرعة محاكاة**. No claim of live sensor data.
- **No measured latency.** Only "capstone design target: < 10 ms fast-path arbitration".
- **No fabricated post-action readings.** Steps 4–5 of the sequence stay conditional and pending.
- **Actuator ownership:** ECController *requests* dilution; ReservoirAgent owns the refill action.
- **No pre-emptive dosing:** pH 6.42 is in range → MONITOR. The architecture requires confirmed
  out-of-range readings before dosing.
- Confidence values, where shown, are qualitative and labelled simulated.
- **6 active + 6 idle + Orchestrator active = 13 agents.**

---

## Bilingual rule

All three screens carry Arabic and English.

- **Arabic carries the narrative** — decision, reason, status words.
- **English carries the identifiers** — pH, EC, mS/cm, agent names, field names.
- **Western digits in both** — 6.42, 2.41, 62 %, 21 L. No conversion risk.

Each artboard has a `showArabic` toggle. Under time pressure, Arabic stays on the screen 1
status chips and the screen 3 decision; all Arabic strings live in one place so the cut is
one edit, not a rewrite.

---

## Scope

**In:** one hard-coded scenario with internally consistent simulated values · four variables ·
six active agents · one Orchestrator resolution · one execution sequence.

**Out — do not build, do not promise:** real sensors or hardware · the full 13-agent system
running · any learning, training, prediction or ML model · live data, accounts, settings,
multi-farm support · more than three screens.

---

## Sources

- بطاقة نطاق البناء (W1), Day 3 — binding scope
- HydroMind Prototype Revision Pack
- Day 1 worksheets: empathy map, pain ranking, target-customer card, competitive scan, problem board
- Day 2 worksheets: 10 ideas, impact/effort matrix, solution concept card
- Business Model Canvas
- *HydroMind: Multi-Agent Agentic AI for Autonomous Hydroponic Farming*, Capstone I Final
  Proposal Report, Effat University, 2026 — used for agent names, layer structure, actuator
  ownership, the arbitration rule, and the message schema only. **Its implementation plan is
  not used.**

---

Incident ID threading all three screens: `corr-7f3a91c4`
