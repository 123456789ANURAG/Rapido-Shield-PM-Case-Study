# Rapido-Shield-PM-Case-Study
# Rapido Shield: Making Bike Taxis Safer for Women Riders

**A product management case study by Anurag Tripathi**

📄 **[View the full deck (PDF)](./Rapido-Shield-Case-Study.pdf)**

> Independent case study built from public sources. Not affiliated with or endorsed by Rapido. User personas are working hypotheses that I am validating through interviews.

---

## TL;DR

Rapido does about 6.5 million rides a day, and in big cities women book roughly a third of them. A bike-taxi ride can go wrong at three moments: **pickup, the ride itself, and after the drop**. At each one, today's safety features wait for the rider to act.

**Rapido Shield** shifts that burden from the rider to the platform, with three layers:

| Layer | Moment | Approach |
|---|---|---|
| **Verified Pickup** | Pickup | AI face match + number-plate OCR before the ride can start |
| **Ride Guardian** | During the ride | AI anomaly detection on route and stops, with a silent check-in |
| **Closed Loop** | After the drop | Contact channels close after the trip; exact address hidden |

---

## 1. Understanding the problem

**Why now**
- ~6.5M daily rides (March 2026) and a $3B valuation after a $240M round (May 2026)
- ~35% of rides in big cities are booked by women (co-founder, 2025)
- MoRTH's new clause 15.6 requires apps to let women choose a woman driver, where available
- Karnataka halted bike taxis for months in 2025; the 2025 Aggregator Guidelines list safety failures as grounds for suspension

For bike taxis, safety is not just a feature. It is the licence to operate.

**Where trust breaks (from reported incidents)**
1. **Pickup:** a captain arrives on a different bike from the one in the app. The rider has to notice the mismatch herself.
2. **The ride:** harassment or rash driving. An SOS button exists, but pressing it while seated behind the captain is the hardest moment to act.
3. **After the drop:** the captain knows where she lives. Women have reported unwanted messages after the trip.

**Problem statement:** How might Rapido make every bike ride verifiably safe for women riders, without adding friction that costs captains rides or riders time?

## 2. Users

| Persona | Job to be done | Core fear |
|---|---|---|
| Late-shift commuter (primary) | Get home fast and cheap without feeling exposed | "Is this even the right person?" |
| Tier-2 city student | Prove to her family the ride is safe | Her number and address are now known |
| Full-time captain (supply side) | Complete more rides per hour | A false complaint or a bad model blocks his ID |

A safety product that ignores the captain fails twice: captains work around it, and supply drops at night when riders need it most.

**Key insight:** every current feature (OTP, SOS, number masking, night call-back) is reactive and rider-triggered. The opportunity is for the platform to verify and watch, so she doesn't have to.

## 3. Solution

### Verified Pickup
- **Input:** captain selfie + number-plate photo at pickup
- **AI:** face match against KYC photo; plate OCR against the registered vehicle
- **Output:** a match unlocks the ride OTP, and the rider sees a "Verified" badge
- **Low confidence:** the rider sees the live photo and confirms herself. Never a silent pass.
- **Friction budget:** under 15 seconds added per pickup, or it doesn't ship

### Ride Guardian
- **Input:** live GPS, planned route, speed, stop duration, time of day
- **AI:** anomaly score for off-route distance, unexplained stops, destination changes
- **Output:** a silent check-in disguised as a "rate your route" prompt. No response in 45s escalates to the safety desk.
- **v1 scope:** women riders, bike rides, 8 PM to 6 AM, opt-out available

### Closed Loop
- Masked calls and chat close 10 minutes after drop
- Captain's trip history shows the locality, not the exact pin
- One-tap "captain contacted me after the ride" report goes to a priority queue

### Human-in-the-loop design
AI speeds up the safety team: it builds the incident view on SOS, spots patterns across complaints, summarises opt-in recordings and drafts police reports. People make the final call on anything that affects a person, such as suspending a captain or escalating to police.

## 4. Model limits and evaluation

**Known failure modes:** low light and helmets reduce face-match accuracy; GPS drift in old-city lanes looks like a detour; legitimate detours; dirty or non-standard plates.

**Evaluation plan**
- **Offline:** labelled pickup photos, target false-reject rate under 2%
- **Shadow mode (4 weeks):** Guardian scores rides silently; flags are compared with real complaints
- **Online:** alert precision, with alert fatigue capped at 1 check-in per rider per week

## 5. Prioritisation (RICE)

| Feature | Reach | Impact | Confidence | Effort | Score |
|---|---|---|---|---|---|
| Closed Loop | 100% | 2 | 80% | 1.5 | **107** |
| Verified Pickup | 100% | 3 | 70% | 4 | **53** |
| Women-captain matching | 10% | 3 | 80% | 2 | 12 |
| Ride Guardian | 30% | 3 | 50% | 6 | 8 |

*All inputs are estimates for illustration.* Women-captain matching ships regardless of score because clause 15.6 requires it. Ride Guardian goes last because it needs shadow-mode data first.

## 6. Success metrics

**North star:** 7-day repeat rate of women riders on bike taxis, split by day and night.

| Input metrics | Guardrails (must not get worse) |
|---|---|
| Mismatched pickups blocked per 10k rides | Pickup time added by verification |
| Post-ride contact reports per 100k rides | Captain rides per hour and weekly churn |
| Median time from flag to human call | Share of penalties overturned on appeal |
| Share of check-ins that were real issues | Cancellations after captain arrival |

## 7. Launch plan

| Weeks | Phase | Gate to move on |
|---|---|---|
| 0–2 | Discovery: 5 rider + 5 captain interviews | The 3 moments hold up in the data |
| 3–6 | Closed Loop, nationwide behind a flag | Contact reports fall |
| 6–14 | Verified Pickup, one city, night rides, A/B by zone | <15s added, captain churn flat |
| 10–20 | Ride Guardian: shadow mode, then opt-in live | Alert precision meets target |

If a gate fails twice, that layer goes back to discovery.

---

## Sources

- Mint via Hyring: daily rides and MAU, March–May 2026
- Economic Times / Venture Intelligence: $240M round at $3B valuation, May 2026
- YourStory: Pink Mobility and share of women riders (2025)
- MoRTH: Amendment to Motor Vehicles Aggregator Guidelines 2025 (clause 15.6)
- MediaNama: Motor Vehicles Aggregator Guidelines 2025
- Outlook Business, Business Today: Karnataka bike-taxi suspension
- Deccan Herald, Organiser, The Logical Indian, Asianet Newsable: reported safety incidents

---

**Anurag Tripathi** · Aspiring AI Product Manager
[LinkedIn](https://www.linkedin.com/in/anurag-tripathi-974bb5314) · Feedback welcome. Open an issue or message me.
