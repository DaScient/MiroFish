# Seed Corpus — *The Prompt Atlas: Kronos Edition*

> This document is the **single text bundle** ingested by MiroFish's seed
> extraction + GraphRAG layer. It encodes the book's positioning, retail
> footprint, audience, comparable titles, and current press surface so that
> generated agents can react with realistic priors. Edit freely; the simulator
> uses entity extraction over this corpus.

---

## 1. Title, edition, and positioning

- **Title:** The Prompt Atlas — Kronos Edition · 2026
- **Subtitle:** A Guide for AI & Humanity
- **Tagline:** *A living, recursive map for navigating intelligence in motion.*
- **One-sentence pitch:** A book, a living web platform, and an open
  prompt-engineering toolbelt across **14 chapters in 7 parts**, bridging
  economics, ecology, culture, science, psyche, ethics, cosmos, resilience, and
  play to answer one recursive question: *How should intelligence — human or
  artificial — build the future it deserves?*
- **Stance:** Not a manual for machines. A map for minds. Humanistic + technical.
- **Author / imprint:** DaScient Press.

## 2. Retail / distribution metadata

| Channel | Identifier | URL |
|---|---|---|
| Barnes & Noble | EAN `2940185139004` | https://www.barnesandnoble.com/w/?ean=2940185139004 |
| Apple Books    | `id6753342960`      | https://books.apple.com/us/book/prompt-atlas/id6753342960 |
| Amazon         | ASIN `B0G13W7RW4`   | https://www.amazon.com/dp/B0G13W7RW4 |
| Live web companion | —              | https://promptatlas.dascient.org |
| GitHub Pages mirror | —             | https://dascient.github.io/The-Prompt-Atlas |
| Repository | DaScient/The-Prompt-Atlas | https://github.com/DaScient/The-Prompt-Atlas |
| Press      | DaScient Press            | https://dascient.com/press |

Formats: paperback, hardcover, Kindle/ebook. License: code MIT; book © 2026 DaScient Press.

## 3. Structure (14 chapters · 7 parts)

> Use this as the canonical TOC for agent reasoning. Replace placeholders below
> with the final TOC when available; the part titles already match the book's
> framing.

1. **Part I — Economics & Work** *(Ch. 1–2)*: labor, productivity, agency.
2. **Part II — Ecology & Systems** *(Ch. 3–4)*: planetary boundaries, feedback.
3. **Part III — Culture & Story** *(Ch. 5–6)*: narrative, language, art.
4. **Part IV — Science & Method** *(Ch. 7–8)*: epistemology, AI for research.
5. **Part V — Psyche & Ethics** *(Ch. 9–10)*: identity, alignment, virtue.
6. **Part VI — Cosmos & Resilience** *(Ch. 11–12)*: scale, risk, continuity.
7. **Part VII — Play & Practice** *(Ch. 13–14)*: prompt craft, toolbelt, exercises.

Each chapter pairs an essay with a **prompt-engineering toolkit** (the
"recursive map" gimmick). The web companion exposes each toolkit as an
interactive page.

## 4. Representative passages to include

> Paste 1–2 short representative excerpts here from the book's most quotable
> chapters (e.g., a passage from Ch. 1 and a passage from Ch. 14). Keeping
> these short keeps token cost low. Sample placeholders:

- *"The 21st century no longer rewards those who simply adapt — it rewards
  those who imagine adaptation itself."*
- *"A prompt is not a command. It is a coordinate on the atlas of what you
  could become."*

## 5. Target audience (operational)

Used to seed `personas.json` cohort weights:

| Cohort | Why they buy |
|---|---|
| AI practitioners / prompt engineers | Toolkits + recursive framing; ammunition for client work |
| Academics (CS, philosophy, ethics, education) | Cross-disciplinary citation magnet; syllabus-ready |
| Journalists / podcasters / reviewers | "Humanism meets prompt-engineering" is a fresh beat |
| K-12 / higher-ed educators & librarians | Curriculum-ready prompts; institutional adoption |
| Generalist curious readers | Big-idea book in the lineage of *Co-Intelligence* / *The Alignment Problem* |
| BookTok / Bookstagram creators | Aesthetic cover, quotable passages, recursive hook |
| Enterprise L&D / corporate trainers | Workshop material; speaking invitations |
| AI skeptics / critics | Stress-test surface; can be flipped into engaged critics |

## 6. Comparable / adjacent titles (anchor agents in genre space)

- *Co-Intelligence* — Ethan Mollick
- *The Alignment Problem* — Brian Christian
- *The AI Conundrum* — (placeholder; replace with the exact comp you want agents to cite)
- *The Coming Wave* — Mustafa Suleyman
- *Tools and Weapons* — Brad Smith
- *A City Is Not a Computer* — Shannon Mattern (humanistic adjacency)
- *The Beginning of Infinity* — David Deutsch (intellectual adjacency)

## 7. Existing assets to amplify

- Repo with code, prompts, and exercises (already public).
- Live web platform mirroring the chapters as interactive pages.
- DaScient Press infrastructure (mailing list, editorial calendar).
- Author network: prior data-science writing audience.
- Open-source companion = built-in **community-flywheel route**.

## 8. Known constraints / risks

- Crowded "AI book" shelf in 2025–2026; differentiation hinges on the
  **humanistic / cross-disciplinary** angle, not on prompt-engineering tactics.
- Author is not (yet) a household name → earned-media tier is uncertain.
- Apple Books featured-submission timing is opaque.
- AI-skepticism news cycles can suppress launch-week press.

## 9. North-star objective for the simulation

> Maximize a **weighted blend** of:
> - 0.40 × normalized unit sales lift across B&N + Apple Books + Amazon
> - 0.30 × academic adoption signal (syllabus mentions, library acquisitions, citations)
> - 0.20 × tier-weighted earned-media mentions
> - 0.10 × durable community size (Discord/repo stars/newsletter subs)
>
> over a **90-day post-launch window**, subject to a **budget tier** (low / med / high).
