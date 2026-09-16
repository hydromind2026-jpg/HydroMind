# HydroMind — Creative Brief (v2)
### Prototype for StartSmart / تحدي الجامعات 2026 — Jeddah Camp, Day-3 build sprint

**Team:** Amro Yousef (build + present) · Layan Turkistani (scenario, content, verification + present) · Nawar Alimam, Tariq Tadmori (capstone team, not presenting)
**Governing document:** بطاقة نطاق البناء (W1), Day 3 — this brief interprets it, it does not extend it.
**Revision basis:** HydroMind Prototype Revision Pack. Concept unchanged; this version is cleaner, more technically consistent with the capstone architecture, and honest about what is simulated.
**Status:** pre-build. Nothing is built yet.

---

## 1. The one-line

> **HydroMind is the coordination and decision layer between farm intelligence and farm actions.**
> **HydroMind هو طبقة التنسيق واتخاذ القرار بين ذكاء المزرعة وإجراءات المزرعة.**

It sits above the agents that sense and control, and decides what happens together, what happens first, and why.

---

## 2. Core story to preserve

> Separate systems can make locally correct decisions that conflict at the farm level. HydroMind coordinates them into one system-level decision and explains why.
>
> الأنظمة المنفصلة قد تتخذ قرارات صحيحة محليًا لكنها تتعارض على مستوى المزرعة. HydroMind ينسّقها في قرار واحد على مستوى النظام، ويشرح السبب.

---

## 3. Prototype hypothesis

> When an operator sees two individually reasonable requests create a system-level conflict, they should understand the value of a coordination layer without first needing an explanation of multi-agent AI.

This is what the demo is testing. If a judge grasps the value without us explaining agents first, the prototype worked.

---

## 4. What we are building

A three-screen clickable prototype that takes **one realistic Mishkat Farm operating scenario** and walks it through:

1. **Farm Status / حالة المزرعة** — what the farm sees
2. **Agent Analysis / تحليل الوكلاء** — what each agent requests, and where two of them collide
3. **HydroMind Decision / قرار HydroMind** — the one merged, sequenced decision and its reason

Two build sprints: 15 min (9:05–9:20) then 30 min (9:20–9:50). Enough for one working path and nothing else.

---

## 5. Why this screen and not another

From our own Day-1 and Day-2 work:

| Source | What it told us |
|---|---|
| Pain-ranking table (Day 1, Session 2) | "Difficulty coordinating decisions between variables and separate systems" scored **19/20** — the highest-ranked pain. Constant human monitoring 18. Late fault detection 17. |
| Competitive scan (Day 1, Session 3) | **Our Day-1 competitive scan identified coordination as the main gap across the alternatives reviewed** — traditional control "لا ينسق بين الأنظمة"; cloud IoT platforms "القرار يبقى مركزياً". |
| Problem board (Day 1, Session 4) | Our differentiation line: multiple agents cooperate and decide together, on the edge. |
| Empathy map (Day 1, Session 2) | The operator's own words: *"عندي حساسات وأنظمة تحكم، لكن كل جزء يعمل بشكل منفصل."* And his question: *"هل النظام سيتخذ القرار الصحيح إذا تغير أكثر من متغير في نفس الوقت؟"* |

Screens 1 and 3 on their own would resemble the monitoring and control products already on the market. **Screen 2 — a visible conflict between two agents over one shared resource — is the differentiation.** It is the screen to build first and build best.

The riskiest assumption on our problem board is that operators see poor coordination as a real, payable pain. This prototype exists to test that assumption in front of judges and in front of Mishkat Farm.

---

## 6. Audience

**Primary — StartSmart judges.** Technical enough to ask "is this real engineering or a mockup?" They will look for a concrete conflict, a stated resolution rule, a traceable decision, and honesty about what is simulated.

**Secondary — the operator or manager at Mishkat Farm.** He should watch the demo and recognise an ordinary afternoon. If he says *"this happens to me"*, the assumption is validated.

---

## 7. User and job

**Site:** Mishkat Farm, Jeddah — a commercial hydroponic operation.
**User / persona:** **the operator or manager at Mishkat Farm.** A farm is the site; the persona is the person running it. He is the same person described in the Day-1 empathy map and target-customer card. **Never use his name** in any screen, document, or spoken line.

**Job:** Help the farm reach a smart, automatically coordinated decision when a fault occurs or when system variables conflict.

---

## 8. The single message

> **Two correct local decisions. One wrong farm-level outcome. HydroMind merges them into one decision — and explains it.**
> **قراران صحيحان محليًا، ونتيجة خاطئة على مستوى المزرعة. HydroMind يدمجهما في قرار واحد، ويشرحه.**

If an element on any screen does not advance that sentence, it does not ship tonight.

---

## 9. Scope

### In
- One realistic operating scenario, hard-coded, with **internally consistent simulated values**
- Four monitored variables: pH, EC, water level, water temperature
- Six active agents with their observation, request, and status
- **Six active agents, six idle agents, and the Orchestrator active = 13 agents** — the architecture is real, tonight's demonstration is partial
- One Orchestrator resolution: shared-resource merge plus process sequencing
- One execution sequence
- A qualitative comparison against independent control logic

### Out — do not build, do not promise
- Any connection to real sensors or hardware
- The full 13-agent system running
- Any learning, training, prediction, or ML model
- Live data, user accounts, settings, multi-farm support
- More than three screens

*(This out-list is taken from the W1 card, section ٤. Treat it as a contract.)*

---

## 10. Honesty rules — non-negotiable

| Rule | Why |
|---|---|
| Screen 1 carries a visible **SIMULATED FARM STATE / حالة مزرعة محاكاة** marker | No claim of live Mishkat sensor data |
| Anything not computed by a running model is labelled **simulated** or shown as a **design target** | Judges will test this |
| No measured latency claims — use "Capstone design target: <10 ms fast-path arbitration" | We have not measured anything |
| No fabricated post-action readings | The prototype does not simulate outcomes; it shows the decision and the conditional next step |
| The dilution figure is an **approximation** (C₁V₁ ≈ C₂V₂), not literal nutrient-mass conservation | It assumes temperature-compensated EC and roughly linear dilution |
| Confidence and trust values, if shown at all, are labelled simulated and kept qualitative | False precision is worse than no precision |

---

## 11. Success criteria

From the W1 card, section ٦ — the prototype succeeds if it can:

1. Analyse a realistic farm problem ✓
2. Show several agents' decisions ✓
3. Resolve the conflict between them ✓
4. Issue one clear final decision through the Orchestrator ✓

Plus two we add for the demo to land:

5. A non-technical judge can restate the decision and the reason after watching once.
6. Screen 3's decision is readable from several metres away, in both languages.

**Failure modes to watch:** screen 2 too weak, so the demo reads as a dashboard · the conflict looks manufactured · we imply live sensors · precision we cannot defend · the build runs past 9:50.

---

## 12. Bilingual direction

The interface is **bilingual Arabic + English on all three screens.** The division of labour is fixed:

| Carries | Language | Examples |
|---|---|---|
| The narrative — what happened, what we decided, why | **Arabic leads, English beneath** | decision line, reason paragraph, presenter-facing status words |
| Technical identifiers | **English only** | pH, EC, mS/cm, agent names (`ReservoirAgent`, `Orchestrator`), topic names, field names |
| Numbers | **Western digits in both** | 6.42, 2.41, 62 %, 21 L — identical in either language, no conversion risk |
| Status chips | **Both, stacked** | HIGH / مرتفع · LOW / منخفض · IN RANGE / ضمن النطاق |

**Why agent names stay English:** they are identifiers that must match the capstone report exactly. Each gets a one-line Arabic role label instead (e.g. `ReservoirAgent` — وكيل الخزان).

**Typography:** a proper Arabic face (IBM Plex Sans Arabic, Noto Kufi Arabic, or Tajawal) with `dir="rtl"` on Arabic blocks. Do not let the browser fall back to a default — Arabic in a Latin fallback font is the fastest way to look unfinished.

**Layout rule:** Arabic sits above or beside English, never as a tooltip or a toggle. A judge should never have to switch languages to understand the screen.

**Cut rule:** if the build runs long, Arabic stays on **screen 1 status chips** and **screen 3 decision + reason** — the parts read at distance. Agent-card Arabic role labels are the first Arabic to go. Keep all Arabic strings in one object in the code so this is a one-line cut, not a rewrite.

---

## 13. Tone and visual direction

**Tone:** operational, not futuristic. A control room, not a product video. Calm, confident, and quiet enough that the conflict is the loudest thing on screen.

**Visual:**
- Dark operational theme — reads at distance during a معرض walk-through
- Screen 1: four large tiles, state chips visible in colour **and** words
- Screen 2: the hero conflict rendered as **two large requests converging on one shared resource**, with an unmistakable incompatibility marker between them; the four supporting agents in a smaller row beneath
- Screen 3: **Decision → Why → Execution.** Technical trace lives in a small optional area, never at the visual centre
- The decision line is the largest type in the whole prototype

---

## 14. Content rules

- Every number on screen must be internally consistent and survive a judge checking the arithmetic
- Agent names match the capstone report exactly: pHController, ECController, WaterTemp, Reservoir, LightCycle, NutrientPlanner, GrowthMonitor, AnomalyResolution, CropState, YieldPredictor, ResourceOptimizer, AnomalyLearner, Orchestrator
- The arbitration rule appears verbatim: **Safety > Crop Health > Resource Efficiency > Optimisation** / **السلامة > صحة المحصول > كفاءة الموارد > التحسين**
- One incident ID threads all three screens: `corr-7f3a91c4`
- Actuator ownership is respected: **ECController requests dilution; ReservoirAgent owns the refill action.** No agent operates hardware it does not own
- Never write "detected by sensor" — write "simulated reading"

---

## 15. Roles tonight

| Role | Who | What |
|---|---|---|
| Account representative | Amro | Builds in Claude, applies edits, saves working versions to GitHub |
| Content and testing | Layan | Prepares the scenario and the pH / EC / water / temperature values, verifies agent and Orchestrator decisions are correct and legible, owns the Arabic copy |
| Testing and scope guard | Amro + Layan | Test after every step, log errors, keep the build inside tonight's single task |
| Presenting | Amro + Layan | 2-minute walk-through |
| Capstone context | Nawar, Tariq | Not part of the competition build; the four-person capstone team continues in parallel |

---

## 16. Guardrails

1. **If a sprint runs long, shrink the supporting-agent row — never cut the hero conflict.**
2. No new variables beyond pH, EC, water level, water temperature.
3. Prepared honest answer for "is this connected to a real farm?": *"No. This is the coordination layer running on a simulated farm state, using Mishkat Farm's operating ranges. Sensors, the full agent stack, and the learning layer are the capstone build. This prototype demonstrates the coordination logic."*
4. The moment the four W1 success criteria can be demonstrated end to end, **stop building and rehearse.**

---

## 17. Sources

- بطاقة نطاق البناء (W1) — Day 3, Jeddah camp — *binding scope*
- HydroMind Prototype Revision Pack — *governs this version*
- أدوات اليوم الأول (Day 1): empathy map, pain ranking, target-customer card, competitive scan, problem board
- أدوات اليوم الثاني (Day 2): 10 ideas, impact/effort matrix, solution concept card
- Business Model Canvas — HydroMind
- *HydroMind: Multi-Agent Agentic AI for Autonomous Hydroponic Farming*, Capstone I Final Proposal Report, Effat University, 2026 — **used for agent names, layer structure, actuator ownership, the arbitration rule, and the message schema only. Its implementation plan is not used.**
