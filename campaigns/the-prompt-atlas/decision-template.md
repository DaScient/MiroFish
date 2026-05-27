# Marketing Route Recommendation — *The Prompt Atlas*
> One-page output to be filled in after the simulation tournament completes.
> Keep to a single page. Anything that doesn't fit goes into an appendix.

**Tournament window:** `<YYYY-MM-DD>` → `<YYYY-MM-DD>`
**Sims run:** `<N>` single-route · `<M>` bundle · `<K>` adversarial
**Aggregate engine cost:** USD `<…>`
**Confidence:** ☐ High  ☐ Medium  ☐ Low *(based on variance across repeats)*

---

## 1. Top 3 routes per objective

| Objective       | #1 (id · score) | #2 | #3 |
|-----------------|-----------------|----|----|
| Media outreach  |                 |    |    |
| Academic impact |                 |    |    |
| Book sales      |                 |    |    |

## 2. Recommended 90-day bundle

- **Bundle id:** `<from routes.yaml `bundles:`>`
- **Budget tier:** ☐ low ($5k)  ☐ medium ($25k)  ☐ high ($100k)
- **Risk-adjusted score:** `<mean − 1σ across repeats>`
- **Rationale (≤3 sentences):**

  > …

## 3. Highest-leverage message framings *(from agent interviews)*

| Audience cohort       | Winning framing      | Source agent IDs |
|-----------------------|----------------------|------------------|
| AI practitioners      |                      |                  |
| Academics             |                      |                  |
| Journalists           |                      |                  |
| Generalist readers    |                      |                  |
| BookTok creators      |                      |                  |
| Enterprise L&D        |                      |                  |

## 4. Pre-mortem — what would make this plan fail

| Failure mode (from metrics.md §10) | Likelihood | Mitigation                |
|-------------------------------------|------------|---------------------------|
| Wrong-cohort capture                | L/M/H      |                           |
| Echo-chamber decay                  |            |                           |
| Skeptic backlash                    |            |                           |
| Channel mismatch                    |            |                           |
| Saturation (half-life < 5d)         |            |                           |
| Budget waste                        |            |                           |

## 5. KPI tripwires *(if not hit by Day 30 → re-simulate)*

| KPI                                  | Day-30 target | Tripwire action            |
|--------------------------------------|---------------|-----------------------------|
| Earned-media tier-weighted mentions  |               | Re-run with A2/A3 swapped in |
| Academic adoption intents            |               | Increase B3 desk-copy volume |
| Amazon weekly rank (best-of-30d)     |               | Activate C1 BookTok flight   |
| Apple Books featured submission ack. |               | Pivot to C3 paid retailer    |
| Discord MAU (community route)        |               | Re-evaluate D2 cadence       |

---

### Appendix A — full tournament table
*(attach the JSON aggregate from prediction-prompt.md "Cross-run aggregation prompt")*

### Appendix B — top agent interview transcripts
*(top journalist, top academic, top skeptic — full chat transcripts)*
