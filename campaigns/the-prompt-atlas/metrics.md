# Metrics — definitions, extraction rules, and ROI formula

This file defines every metric the ReportAgent is asked to compute and the
exact event in MiroFish's action log it should bind to. Stable definitions
make runs comparable across weeks and reruns.

---

## 1. Action-log event taxonomy (from MiroFish `actions.jsonl`)

| Event kind (in `action`)         | Counts toward |
|----------------------------------|---------------|
| `create_post`, `repost`, `quote_post` | reach, earned-media, share_actions |
| `like_post`, `like_comment`           | sentiment, penetration |
| `create_comment`, `reply_to_comment`  | sentiment, penetration |
| `follow`, `subscribe`                 | community size |
| custom action `purchase_intent`       | sales_lift (see §3) |
| custom action `adopt_for_course`      | academic adoption |
| custom action `request_review_copy`   | academic adoption |

> If MiroFish's runner does not natively emit `purchase_intent` /
> `adopt_for_course`, treat any post or comment whose embedding cosine ≥ 0.70
> to a canonical intent sentence ("I'll buy this", "I'll assign this") as an
> event of that kind. The ReportAgent should apply this rule explicitly.

---

## 2. Tier weights for journalists / reviewers

| Tier | Examples                                  | Weight |
|------|-------------------------------------------|--------|
| T1   | NYT, Wired, Atlantic, Lex Fridman, Ezra Klein, Hard Fork | 1.0 |
| T2   | MIT Tech Review, Noema, Cognitive Revolution, Latent Space | 0.5 |
| T3   | Niche newsletters, smaller podcasts, regional press | 0.2 |

Each journalist-cohort agent has a `tier` attribute (auto-assigned during
profile generation; bias 20% T1 / 40% T2 / 40% T3).

`tier_weighted_mentions = Σ over journalist agents who posted ≥1 post · tier_weight`

---

## 3. Sales lift

Per retailer:

```
sales_lift_pct(retailer) = (purchase_intents_route(retailer) − purchase_intents_baseline(retailer))
                           / max(1, purchase_intents_baseline(retailer))
```

A `purchase_intent` is bound to a retailer by whichever retailer URL/keyword
appears in the originating post or in the agent's bio (`amazon.com`,
`barnesandnoble.com`, `apple.com/books`). If none, distribute proportionally
to a 60/25/15 baseline (Amazon / B&N / Apple Books).

---

## 4. Academic adoption signal

```
academic_score = 1.0 * adopt_for_course
               + 0.6 * request_review_copy
               + 0.4 * share_action_by_academic_cohort
               + 0.8 * library_acquisition_intent
```

Where `library_acquisition_intent` is any educator/librarian-cohort agent
posting/commenting to the effect of "I'll request this for our collection".

---

## 5. Sentiment

Per round, run the simulator's built-in sentiment classifier (or fall back
to an LLM-as-judge score in [-1, 1]) on every text emission. Aggregate:

- `overall_final` — mean over the final round.
- `by_cohort` — mean over the final round, segmented by `cohort_id`.
- `weekly_trajectory` — array of 13 entries (90 days ÷ 7).

---

## 6. Penetration

```
penetration(cohort) = |{agents in cohort with ≥1 positive action}|
                    / |agents in cohort|
```

A *positive action* = like / share / comment-positive / purchase_intent /
adopt_for_course / request_review_copy / follow author.

---

## 7. Decay half-life

Fit `engagement_t = A · exp(-λ t)` to weekly engagement counts.
`half_life_days = ln(2) / λ · 7`. A long half-life (>30d) signals durability;
a short one (<7d) signals a flash-in-the-pan route.

---

## 8. Objective score (normalized blend)

```
objective_score = 0.40 * norm(sales_lift_index)
                + 0.30 * norm(academic_score)
                + 0.20 * norm(tier_weighted_mentions)
                + 0.10 * norm(community_size_delta)
```

Where `norm(x) = x / max_across_comparison_set(x)`. The comparison set is all
runs at the same budget tier within the same tournament wave.

`sales_lift_index = 0.55*amazon + 0.30*bn + 0.15*apple` weighted by historical
retailer share for nonfiction big-idea books; revise after first 30 days of
real-world data.

---

## 9. ROI ranking

```
ROI(route, tier) = objective_score(route, tier) / budget_tier_dollars[tier]
```

Use `risk_adjusted_score = mean(objective_score) − stddev(objective_score)`
as the **primary** rank metric when there are ≥3 repeats.

---

## 10. Failure-mode taxonomy

When the ReportAgent surfaces failure modes, force-classify into one of:

1. **Wrong-cohort capture** — engagement concentrated in a cohort that doesn't
   convert (e.g., big AI-skeptic activity, no sales).
2. **Echo-chamber decay** — repeated shares within one cohort, no diffusion.
3. **Skeptic backlash** — negative-sentiment cascade after a critical post.
4. **Channel mismatch** — message framing doesn't fit the platform/audience.
5. **Saturation** — early engagement, fast decay (half-life < 5 days).
6. **Budget waste** — high spend, no measurable penetration delta vs. baseline.

These map cleanly to the mitigations in `decision-template.md`.
