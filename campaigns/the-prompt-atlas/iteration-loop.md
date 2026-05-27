# Iteration Loop & KPI Tripwires

MiroFish is most useful as a **continuous decision-support tool**, not a
one-shot oracle. Every 30 days, re-ingest real-world signals and re-run the
relevant subset of the tournament.

---

## Day 0 — Launch

- Lock the recommended bundle from `decision-template.md` §2.
- Snapshot baseline real-world metrics (Amazon BSR, B&N pre-orders, Apple
  Books rank, Goodreads adds, repo stars, newsletter subs).
- Tag the simulation run that produced the recommendation as `RUN_OF_RECORD`.

## Day 30 — First checkpoint

For each KPI in `decision-template.md` §5:

1. Compare actual to target.
2. If **hit** → keep the route, increase its budget allocation by +20%.
3. If **missed** → execute the listed tripwire action and queue a re-sim.

Re-ingest the following as **new seed material** before re-running:

- Sales data from each retailer (or proxy: Amazon BSR weekly).
- Press hits (URL, outlet tier, sentiment).
- Academic mentions (Google Scholar alerts, syllabus references).
- Community size deltas (Discord MAU, repo stars, newsletter subs).
- Notable adversarial events that actually occurred.

Re-run only the *single-route* simulations whose tripwires fired, plus a
bundle re-evaluation with the same fixed seeds. Cost guardrail: ≤ USD 100.

## Day 60 — Halfway recalibration

- Refit `metrics.md §8` retailer share weights from observed sales mix.
- Reassess persona shares in `personas.json` if the actual audience differs
  meaningfully (e.g., far more educator interest than expected → bump
  `educator_librarian` share from 0.10 to 0.15).
- Re-run the **top 3 routes + recommended bundle** with the updated personas
  and updated seed corpus. Compare new objective scores to RUN_OF_RECORD.

## Day 90 — Tournament close & next-quarter plan

- Score the actual 90-day blend per `seed-corpus.md §9`.
- Validate MiroFish's *relative* ranking against reality:
  | Pred. rank (sim) | Actual rank | Δ |
- For each route that **beat** its predicted ROI → promote into Q2 plan.
- For each route that **underperformed** by >25% → retire or reframe.
- Rebuild `personas.json` from any new evidence (e.g., a surprise viral
  BookTok hit means the `booktok_creator` cohort needs richer personas).

---

## Standing automation suggestions

- **Daily action-log archive.** Cron archive of `actions.jsonl` from each
  active simulation to long-term storage so reruns can replay.
- **Weekly Goodreads/Amazon scrape** (respecting ToS) into a CSV that feeds
  the next re-seeding.
- **Press-hit ingestion bot.** Watch a small list of outlets + podcast feeds
  for the book title; auto-attach to the next seed corpus revision.
- **Quarterly model swap test.** Re-run the baseline with a different LLM
  (e.g., Qwen-plus → GPT-4o-mini) on the same seed; record whether route
  *rankings* are stable (they should be — that is the headline epistemic test
  of this whole program).
