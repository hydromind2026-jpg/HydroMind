# HydroMind — Prototype Storyboard (v2)
### Three screens · one scenario · one coordinated decision · bilingual AR/EN
**Scope source:** بطاقة نطاق البناء (W1), Day 3 · **Revision basis:** HydroMind Prototype Revision Pack
**Companion:** HydroMind Creative Brief v2 · **Build budget:** 15 min + 30 min · **Status:** spec only

---

## 0. The scenario

**Mishkat Farm, Jeddah.** Four-zone NFT rig, shared 100 L reservoir, butterhead lettuce, vegetative stage. A hot afternoon. This is a **realistic operating scenario built from Mishkat Farm's operating ranges** — not a recorded historical event.

Water has been evaporating faster than usual. As volume drops, the nutrient solution concentrates. Four things become true at once:

- the reservoir is **low**
- EC is **high** — the same nutrients in less water
- water temperature is **high**
- pH is **still in range**, but trending upward

Each has an agent watching it. Two of those agents are about to request **the same physical resource** — the reservoir — for different local goals. Individually both requests are reasonable. Executed independently, they compete.

That is the entire demo.

### Reading set — use these values consistently on all three screens

| Variable | Reading | Target / bound | Prototype interpretation |
|---|---|---|---|
| pH | **6.42** ↗ | Target 5.5 – 6.5 | **In range**; rising trend; monitor |
| EC | **2.41** mS/cm | Target 1.80 ± 0.10 | **High**; dilution request |
| Water level | **62 %** = 62.0 L | Target 70 – 90 % | **Low**; refill request |
| Water temp | **24.6 °C** | Target 18 – 22 °C | **High**; chiller action |
| Safety mode | **NORMAL** | No safety bound crossed | Coordination problem, not emergency |

**Three readings are outside their operating targets. pH is not one of them.** Say it that way.

**Incident ID:** `corr-7f3a91c4` — appears on all three screens.

### Dilution estimate

> **Assumption:** temperature-compensated EC and approximately linear dilution for this prototype calculation. This is a **simplified dilution estimate**, not literal nutrient-mass conservation.

```
C₁V₁ ≈ C₂V₂
2.41 × 62  ≈  1.80 × V₂
V₂ ≈ 83.0 L
Fresh water required ≈ 21.0 L
```

**Why uncoordinated requests are undesirable (illustrative only — not a measured outcome):**
ReservoirAgent's +28 L request alone takes the reservoir to 90 L. If independent requests compete for the same reservoir, volume is driven toward the **95 % hardware float cutoff**. At 95 L the same simplified estimate gives EC ≈ **1.57 mS/cm** — below the target band. Use this to explain *why* coordination matters; do not present it as something the prototype measured.

---

## 1. Screen 1 — Farm Status / حالة المزرعة

> **EN:** *"This is the farm right now. Four readings. Three are outside their operating targets, but none has crossed a safety limit."*
> **AR:** *«هذه حالة المزرعة الآن. أربع قراءات، ثلاث منها خارج النطاق التشغيلي، ولم يتجاوز أي منها حد الأمان.»*

```
┌────────────────────────────────────────────────────────────────┐
│  MISHKAT FARM · JEDDAH  ·  مزرعة مشكاة — جدة                   │
│  4-zone NFT · 100 L reservoir            MODE: NORMAL / طبيعي  │
├────────────────────────────────────────────────────────────────┤
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐           │
│  │   pH    │  │   EC    │  │  WATER  │  │  TEMP   │           │
│  │         │  │         │  │ المياه  │  │ الحرارة │           │
│  │  6.42 ↗ │  │  2.41   │  │  62 %   │  │ 24.6 °C │           │
│  │         │  │  mS/cm  │  │ 62.0 L  │  │         │           │
│  │IN RANGE │  │  HIGH   │  │   LOW   │  │  HIGH   │           │
│  │ضمن النطاق│  │ مرتفع   │  │ منخفض   │  │ مرتفع   │           │
│  │5.5 – 6.5│  │1.80±0.10│  │ 70–90 % │  │ 18–22°C │           │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘           │
├────────────────────────────────────────────────────────────────┤
│ 6 agents responded · 1 cross-system conflict detected          │
│ 6 وكلاء استجابوا · تعارض واحد بين الأنظمة                       │
│ corr-7f3a91c4          SIMULATED FARM STATE / حالة مزرعة محاكاة │
│                        [ View Agent Decisions → عرض قرارات الوكلاء ] │
└────────────────────────────────────────────────────────────────┘
```

### Content rules
- Each tile: label (EN + AR) · value · unit · state chip (EN + AR) · target band. Nothing else.
- Out-of-range tiles differ by **colour and word**, so the state survives a photo and colour-blind viewing.
- The pH tile reads **IN RANGE / ضمن النطاق** with a trend arrow — not an alarm. This proves the system distinguishes *wrong* from *heading wrong*, and it is the first thing a careful judge will check.
- Mode reads **NORMAL**, not ALERT. Coordination failures happen on ordinary days; that is the insight.
- `SIMULATED FARM STATE / حالة مزرعة محاكاة` is permanently visible. Non-negotiable.

### One interaction
`View Agent Decisions →` advances to screen 2. The only control on this screen.

### Do not build
Sparklines, history, per-zone breakdown, camera feed, settings, login, any second alert.

---

## 2. Screen 2 — Agent Analysis / تحليل الوكلاء
### ★ The hero screen. Build it first, build it best.

> **EN:** *"The agents are individually reasonable. The problem is that two of them are requesting the same physical resource for different local goals."*
> **AR:** *«كل وكيل منطقي بمفرده. المشكلة أن وكيلين يطلبان نفس المورد المادي لهدفين مختلفين.»*

### Hero layout — two large requests converging on one shared resource

The conflict must be legible from several metres. Not a label — a **collision**.

```
   ReservoirAgent                                    ECControllerAgent
   وكيل الخزان                                       وكيل التحكم في EC

   Level 62 % is below                              EC 2.41 is above
   operating target                                 the 1.80 target
   الخزان منخفض                                      التركيز مرتفع

   ┌──────────────────┐                        ┌──────────────────┐
   │  REQUEST REFILL  │                        │ REQUEST DILUTION │
   │   طلب تعبئة       │                        │   طلب تخفيف       │
   │     + 28 L       │                        │    ≈ + 21 L      │
   └────────┬─────────┘                        └────────┬─────────┘
            │                                           │
            └──────────────►  ⚠  ◄──────────────────────┘
            ⚠ SHARED-RESOURCE CONFLICT / تعارض على مورد مشترك
                  ┌────────────────────────────┐
                  │   SHARED RESOURCE          │
                  │   RESERVOIR · 100 L        │
                  │   المورد المشترك — الخزان   │
                  └────────────────────────────┘
```

**Both requests are P2 Crop Health.** Priority alone does not separate them — and that is the point. Independent control logic has no mechanism to notice they act on the same resource.

**Actuator ownership (get this right — a judge will check):** ECController **requests dilution equivalent to ≈ +21 L fresh water**. It does not operate the solenoid. **ReservoirAgent owns the refill action.**

### Supporting agents — a smaller row beneath the hero conflict

| Agent | Belief | Request / recommendation | On-card label | Status |
|---|---|---|---|---|
| **WaterTempAgent** · وكيل حرارة الماء | 24.6 °C is above the 22 °C ceiling | Chiller ON until temperature returns to band | `CHILLER ON` · تشغيل المبرّد | **EXECUTE** / تنفيذ |
| **pHControllerAgent** · وكيل التحكم في pH | pH 6.42 is within band but trending upward | **Monitor; re-check after refill and mixing. No dose now.** | `IN RANGE → MONITOR` · ضمن النطاق ← مراقبة | **OBSERVE** / مراقبة |
| **NutrientPlannerAgent** · وكيل تخطيط التغذية | A volume change invalidates immediate chemistry decisions | Merge the water action; mix; re-measure; dose only if needed | `REFILL → MIX → RE-MEASURE` · تعبئة ← مزج ← إعادة قياس | **PLAN** / خطة |
| **AnomalyResolutionAgent** · وكيل تشخيص الأعطال | Evaporation is plausible, but evidence is insufficient for a fault declaration | Keep the diagnosis provisional; collect more evidence | `EVAPORATION PLAUSIBLE · NO FAULT DECLARED` · تبخّر محتمل · لم يُعلن عطل | **HOLD** / تعليق |

The **On-card label** column is the literal text that ships on screen — short enough to read at a glance. The belief and request columns are reference for the build, not screen copy.

**pH is context, not a second hero conflict.** The capstone logic requires confirmed out-of-range readings before dosing, and pH 6.42 is in range. A pre-emptive dose here would contradict our own architecture — and it would dilute the one conflict we want the judge to see.

**AnomalyResolution's restraint is a feature, not a gap.** Point at it in the demo: the system also knows when it does not know enough to declare a fault.

### Architecture strip (bottom)

```
Idle this cycle: LightCycle · GrowthMonitor · CropState · YieldPredictor ·
                 ResourceOptimizer · AnomalyLearner
6 active | 6 idle | Orchestrator active = 13 agents
6 نشط | 6 خامل | المنسّق نشط = 13 وكيلاً
```

Scope honesty and credibility in one line: the architecture is thirteen agents, six had something to say about this scenario, and we are not pretending otherwise.

### Confidence — if shown at all
Qualitative only, and labelled: `Confidence (simulated): High / Medium / Provisional`. No decimals. Drop trust scores entirely for this build — they only matter in consensus, which is not triggered here.

### One interaction
`ORCHESTRATOR — RESOLVE → / المنسّق — احسم التعارض` advances to screen 3.

### Do not build
Clickable cards, expandable detail, message logs, live updates, animation beyond the conflict marker.

---

## 3. Screen 3 — HydroMind Decision / قرار HydroMind

> **EN:** *"HydroMind does not execute both requests. It recognizes that they act on the same resource, merges them, and sequences the remaining actions around the farm physics."*
> **AR:** *«HydroMind لا ينفّذ الطلبين. يدرك أنهما يعملان على نفس المورد، فيدمجهما، ثم يرتّب باقي الإجراءات وفق فيزياء المزرعة.»*

**This is a decision screen, not a report page.** Three blocks: Decision → Why → Execution. Everything technical goes in a small optional area at the bottom.

### Block 1 — THE DECISION (largest type in the prototype)

> # ONE COORDINATED DECISION
> # قرار واحد منسّق
>
> ## ADD 21 L ONCE · إضافة 21 لتر مرة واحدة
> **Reservoir: 62 L → ≈ 83 L  |  Estimated EC: 2.41 → ≈ 1.80 mS/cm**
> **الخزان: 62 → ≈ 83 لتر  |  EC المتوقع: 2.41 → ≈ 1.80**
>
> ▸ **Parallel action / إجراء متوازٍ:** CHILLER ON · تشغيل المبرّد
> ▸ **HOLD CHEMICAL DOSING UNTIL MIXING COMPLETES · إيقاف الجرعات الكيميائية حتى اكتمال المزج**

The chiller is shown as **parallel**, not as step one of a chain — it acts on temperature, not on the contested resource, so it has no reason to wait.

Use "about / حوالي" on the outcome figures. They are estimates from the dilution approximation, not predictions the prototype computed.

### Block 2 — WHY / لماذا اتخذ HydroMind هذا القرار

> **EN:** The low reservoir and the high EC are not two independent problems requiring two separate water actions. They share the same physical resource. HydroMind merges the requests into one refill/dilution action, then delays chemical dosing until the new volume has mixed and the system is measured again.
>
> **AR:** انخفاض الخزان وارتفاع EC ليسا مشكلتين منفصلتين تحتاجان إجراءين للمياه. كلاهما يتعلق بنفس المورد. يدمج HydroMind الطلبين في إجراء تعبئة/تخفيف واحد، ثم يؤجّل أي جرعة كيميائية حتى يمتزج الحجم الجديد وتُعاد القياسات.

### Block 3 — EXECUTION SEQUENCE / تسلسل التنفيذ

```
   ①              ②              ③            ④              ⑤
Chiller ON  →  Add 21 L   →     Mix     →  Re-measure  →  Dose only
                                                           if needed
تشغيل المبرّد   إضافة 21 لتر      مزج       إعادة القياس   جرعة عند الحاجة
```

Steps ④ and ⑤ are shown as **conditional and pending** — the prototype does not claim what the re-measurement will say. Label the mixing wait as *capstone design value: 5–10 min full-loop homogenisation*, not as a measured duration.

Agents whose requests were not executed as submitted get honest status, so nothing silently disappears:
`ReservoirAgent · MERGED / مدموج` — *combined into the single water action*
`pHControllerAgent · DEFERRED / مؤجّل` — *re-check scheduled after mixing, not ignored*

### Block 4 — Technical trace (small, bottom corner, not the visual centre)

```
Arbitration rule    Safety > Crop Health > Resource Efficiency > Optimisation
                    السلامة > صحة المحصول > كفاءة الموارد > التحسين
Conflict resolution Shared-resource merge + process sequencing
Mode                NORMAL — no safety bound breached
Consensus           Not triggered (no mode change, no harvest decision)
Latency             Capstone design target: < 10 ms fast-path arbitration
Incident ID         corr-7f3a91c4
Note                Confidence values shown are simulated
```

### Block 5 — Closing comparison (qualitative)

| Independent control logic | HydroMind coordination |
|---|---|
| Two separate water requests can compete for the same reservoir. | One merged water action, then mix and re-measure before any chemical dose. |
| منطق تحكم مستقل: طلبان منفصلان للمياه قد يتنافسان على نفس الخزان. | تنسيق HydroMind: إجراء مياه واحد مدموج، ثم مزج وإعادة قياس قبل أي جرعة كيميائية. |

> **EN:** *"Same sensors. Same actuators. The difference is coordination."*
> **AR:** *«نفس الحساسات. نفس المشغّلات. الفرق هو التنسيق.»*

---

## 4. Flow and demo script

```
Farm Status ──[View Agent Decisions]──▶ Agent Analysis ──[Resolve]──▶ HydroMind Decision
```

Three screens, two clicks, no back navigation.

| Time | Screen | Say |
|---|---|---|
| 0:00 – 0:20 | 1 | Mishkat Farm, Jeddah. Four readings — **three outside operating targets, none past a safety limit.** An ordinary hot afternoon, not an emergency. |
| 0:20 – 1:10 | 2 | Six agents responded. Land the hero conflict: **two agents, both reasonable, requesting the same reservoir for different reasons.** Then the restraint cases — pH is in range so it monitors instead of dosing; Anomaly Resolution declines to declare a fault without evidence. Point at the architecture strip: *thirteen agents, six had something to say tonight.* |
| 1:10 – 1:45 | 3 | The decision, then the reason, then the five-step sequence. Mention the arbitration rule. Do not linger on the trace. |
| 1:45 – 2:00 | 3 | The comparison, then the closing line — in Arabic. |

---

## 5. Agent message format (for the build)

Six agent objects plus the Orchestrator output, hard-coded. Fields follow the capstone schema.

```json
{
  "sender": "ECController",
  "sender_ar": "وكيل التحكم في EC",
  "correlation_id": "corr-7f3a91c4",
  "priority": "P2",
  "payload_type": "request",
  "payload": {
    "reading": 2.41,
    "unit": "mS/cm",
    "target": 1.80,
    "belief_en": "EC 2.41 is above the 1.80 target.",
    "belief_ar": "التركيز 2.41 أعلى من المستهدف 1.80.",
    "request_en": "Request dilution equivalent to about +21 L fresh water.",
    "request_ar": "طلب تخفيف بما يعادل حوالي +21 لتر ماء عذب.",
    "owns_actuator": false
  },
  "confidence_simulated": "High",
  "status": "CONFLICT"
}
```

Valid `status`: `CONFLICT` · `EXECUTE` · `OBSERVE` · `PLAN` · `HOLD` · `MERGED` · `DEFERRED` · `IDLE`

Orchestrator output adds: `arbitration_rule`, `resolution_method`, `merged[]`, `deferred[]`, `execution_sequence[]`, `mode`, `latency_note`.

**Keep all Arabic strings in one object** so the Arabic layer can be reduced in one edit if time runs short.

---

## 6. Build order (protects the 45 minutes)

**Sprint 1 — 9:05 to 9:20**
1. Data file: six agent objects + Orchestrator output, bilingual. Layan verifies every number and every Arabic line.
2. Screen 2 hero conflict: two request blocks, shared-resource block, incompatibility marker.

*Exit check: is the conflict readable from across the room? If no, fix before continuing.*

**Sprint 2 — 9:20 to 9:50**
3. Screen 2 supporting-agent row + architecture strip
4. Screen 3 — Decision → Why → Execution (trace block last)
5. Screen 1 — four tiles (fastest screen, build it last)
6. Wire the two buttons
7. Closing comparison — **first thing to cut**

*Exit check: all four W1 success criteria demonstrable end to end. Then stop and rehearse.*

**Cut list, in order:** closing comparison → technical trace block → Arabic on agent cards → supporting agents 4 → 2.
**Never cut:** the hero conflict, the decision line in both languages, the arbitration rule, the SIMULATED marker.

---

## 7. Build acceptance checklist (Layan, before rehearsal)

- [ ] Screen 1 clearly says **SIMULATED FARM STATE / حالة مزرعة محاكاة**
- [ ] Presenter says **three** readings are outside target, not two
- [ ] pHController does **not** dose at pH 6.42 — status is OBSERVE / مراقبة
- [ ] ECController **requests dilution**; ReservoirAgent **owns the refill action**
- [ ] Reservoir +28 L vs EC ≈ +21 L is the single main visible conflict
- [ ] Float/overflow cutoff is **95 %**, not 100 %, wherever shown
- [ ] Dilution is labelled an **approximation** (C₁V₁ ≈ C₂V₂), not nutrient-mass conservation
- [ ] **No "measured 4 ms"** claim anywhere — only "capstone design target < 10 ms"
- [ ] **No fabricated post-action** pH/EC values or time-to-stable figures
- [ ] Any hard-coded confidence values are labelled **simulated** and kept qualitative
- [ ] **6 active + 6 idle + Orchestrator active = 13 agents**
- [ ] Screen 3 is readable from a distance and has one unmistakable final decision
- [ ] Arabic renders in a proper Arabic face with correct RTL direction on every screen
- [ ] `corr-7f3a91c4` appears on all three screens
- [ ] Every agent on screen 2 resolves to an explicit status on screen 3
- [ ] The farm manager's name appears nowhere
- [ ] The complete demo still fits in two minutes
- [ ] No extra screens, settings, login, live feeds, or hardware integration

---

## 8. Prepared answers

**"Is this connected to a real farm?"**
No. This is the coordination layer running on a simulated farm state, using Mishkat Farm's operating ranges. Sensors, the full agent stack, and the learning layer are the capstone build. This prototype demonstrates the coordination logic.

**"Could a normal controller just be programmed to handle this case?"**
Yes. A conventional controller could be manually programmed for this exact scenario. The difference HydroMind is designed to provide is a **general coordination mechanism**: agents submit their local objectives, and the Orchestrator resolves competing actions according to system-level priorities and dependencies. Tonight's prototype demonstrates that coordination logic on one scenario.

**"Why only six agents?"**
Thirteen agents exist in the architecture. Six had something to say about this scenario. Showing all thirteen responding to a water-level event would be dishonest.

**"What happens if the Orchestrator itself fails?"**
The reactive layer is stateless and independent of it. Safety bounds and the hardware watchdog keep working. The farm loses coordination, not control.

**"Where did the 21 L come from?"**
A simplified dilution estimate, C₁V₁ ≈ C₂V₂, assuming temperature-compensated EC and roughly linear dilution. It is a prototype approximation, and we label it as one.
