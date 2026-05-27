# Campaign: *The Prompt Atlas — Kronos Edition*

A turnkey MiroFish simulation package for predicting which marketing routes will
most effectively grow **media outreach, academic/education impact, and book
sales** for [*The Prompt Atlas*](https://github.com/DaScient/The-Prompt-Atlas).

| Retailer | Link |
|---|---|
| Barnes & Noble | https://www.barnesandnoble.com/w/?ean=2940185139004 |
| Apple Books    | https://books.apple.com/us/book/prompt-atlas/id6753342960 |
| Amazon         | https://www.amazon.com/dp/B0G13W7RW4 |
| Live site      | https://promptatlas.dascient.org |

This package is **engine-agnostic**: the JSON/Markdown/YAML files here describe
the seed corpus, persona cohorts, candidate marketing routes, prediction goals,
and experimental matrix. They are designed to be loaded by MiroFish's
`run_parallel_simulation.py` (see `simulation_config.json`) or by any compatible
OASIS-based swarm-simulation runner.

---

## Files in this package

| File | Purpose |
|---|---|
| `README.md`                  | This overview + how-to-run |
| `seed-corpus.md`             | The text bundle uploaded to GraphRAG/seed extraction |
| `personas.json`              | Heterogeneous agent cohorts and their distribution |
| `routes.yaml`                | Catalog of candidate marketing interventions (A/B/C/D, budget tiers) |
| `prediction-prompt.md`       | Natural-language goal handed to ReportAgent |
| `experiments.yaml`           | Experimental design matrix (baseline / single / bundle / adversarial) |
| `metrics.md`                 | Operational metric definitions extracted from each run |
| `decision-template.md`       | One-page "Marketing Route Recommendation" template |
| `iteration-loop.md`          | 30-day KPI tripwires & re-simulation checklist |
| `simulation_config.json`     | MiroFish-ready config skeleton (initial posts, time, agents) |

---

## Quick start (with MiroFish)

```bash
# 1. From the MiroFish project root, configure env vars
cp .env.example .env   # then fill LLM_API_KEY and ZEP_API_KEY
                       # English/marketing nuance → consider a GPT-4-class model

# 2. Install
npm run setup:all

# 3. (Optional) regenerate personas from the seed corpus
#    Edit personas.json to taste, or run MiroFish's profile generator
#    against campaigns/the-prompt-atlas/seed-corpus.md

# 4. Run a baseline simulation (no intervention)
cd backend
uv run python scripts/run_parallel_simulation.py \
    --config ../campaigns/the-prompt-atlas/simulation_config.json

# 5. Run each marketing route in routes.yaml as its own simulation:
#    duplicate simulation_config.json, swap event_config.initial_posts
#    with the route's intervention block, and set a new simulation_id.

# 6. After the simulations finish, use MiroFish's Interview / ReportAgent
#    feature to ask the prompt in prediction-prompt.md against each run.
```

> ⚠️ **LLM cost warning** (from MiroFish README): start with **≤40 rounds** per
> simulation, run small persona pools first (e.g., 60–80 agents), then scale.

---

## Experimental flow

```
                       ┌─────────────────────┐
                       │  Baseline run (B0)  │  organic trajectory
                       └──────────┬──────────┘
                                  │
        ┌─────────────────────────┼──────────────────────────┐
        ▼                         ▼                          ▼
  Single-route runs        Bundle runs              Adversarial runs
  (one per route in        (top-K combos +          (negative-news
   routes.yaml)             "balanced trio")          injection)
        │                         │                          │
        └─────────────────────────┴──────────────────────────┘
                                  │
                                  ▼
                 ReportAgent extracts metrics.md fields
                                  │
                                  ▼
                Aggregate over 3–5 repeats, populate
                       decision-template.md
                                  │
                                  ▼
            30-day real-world test → iteration-loop.md
```

---

## What MiroFish gives us that spreadsheets do not

1. **Emergent word-of-mouth.** Agents talk to each other across rounds, so the
   simulation captures secondary diffusion (a journalist agent reads a tweet
   from a practitioner agent and posts a review).
2. **Cohort-conditional response.** Personas with persistent Zep memory let us
   measure how the same message lands differently with academics vs. BookTok.
3. **Adversarial robustness.** Injecting a skeptic op-ed mid-simulation tells
   us which routes degrade gracefully.
4. **Deep interaction.** After a run, we interview the *top-performing
   journalist agent* to learn what made them cover — concrete copy refinement.

---

## Caveats (read before acting on results)

- MiroFish predicts **relative rankings and failure modes**, not absolute unit
  sales. Treat numbers as ordinal.
- Persona realism = seed quality. Invest most upfront effort in
  `seed-corpus.md` and `personas.json`.
- Validate at least one top-ranked route against a small **real-world test**
  (e.g., book one podcast from the recommended list) before committing budget.
