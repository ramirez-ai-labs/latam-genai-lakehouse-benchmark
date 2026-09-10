# Roadmap — latam-genai-lakehouse-benchmark

Status as of 2026-09-10: Bronze/Silver/Gold notebook on Databricks with a clean architecture
narrative and a production-extension doc. The **Gold layer does not call a model** — "accuracy"
is `0.75 + rand(42)*0.20` minus a hardcoded noise penalty. The framing is good; it needs a real
evaluator underneath and a real dataset.

Goal: a reproducible Lakehouse benchmark that answers one question — **does LatamGPT close the
SV vs PE dialect gap that frontier models leave open?** — with real inference and judge scoring.

---

## P1 — Make the Gold layer real (highest priority)

- [ ] **Real inference in Gold** — replace the `rand()` accuracy with actual model calls on the
      neutral-Spanish rewrite task, for three subjects under test:
      - `latam-gpt/Llama-3.1-70B-LatamGPT-SFT-1.0`
      - GPT-4o
      - Claude
- [ ] **LLM-judge scoring** — score each output on a rubric: meaning preservation, register
      neutrality, slang handled correctly, no hallucinated content. Store per-item scores in
      `latam_gold_eval_runs` (model_name, item_id, rubric dimensions, overall).
- [ ] **Real summary** — `latam_gold_eval_summary` becomes accuracy by {model × region ×
      noise_level} with the SV↔PE gap per model as the headline metric.
- [ ] Commit a rendered results table / screenshot to `docs/` so the finding is visible without
      running the notebook.

## P2 — Dataset

- [ ] Populate `sample_data/dialect_examples.csv` (currently 0 bytes) — move the 10 hardcoded
      rows out of the notebook into the CSV.
- [ ] Grow to ~60–100 items: more countries (add MX, CO, AR, CL), more registers (formal /
      informal / mixed), more task types beyond slang rewrite.
- [ ] Bronze layer loads from the CSV instead of an inline Python list.
- [ ] Add a **Wayra perplexity column in the Silver layer** as a data-quality signal — ties
      this repo to `latam-rag-quality-gate` technically.

## P3 — SDLC (practice what the docs preach)

`docs/production_extension.md` describes CI/CD gating, MLflow, and promotion flows. The repo
should demonstrate at least the entry-level version:

- [ ] `.github/workflows/ci.yml` — lint + a smoke test of the aggregation / gap-calculation
      logic (extract it into a plain `.py` module the notebook imports, so it's testable).
- [ ] `tests/` — unit tests for the judge-score parsing and the summary SQL logic.
- [ ] Optional: MLflow logging of each eval run (model version, dataset version, metrics).
- [ ] Tag a `v0.1` release once P1 lands.
- [ ] Add `CONTRIBUTING.md`.

## P4 — Fixes / hygiene

- [ ] README: broken image link — points to `architecture/lakehouse_eval_architecture.png`,
      actual file is `architecture/lakehouse_diagram.png`.
- [ ] README author block: "Victo Ramirez / AI Architect" → correct spelling, current title,
      add links (org, LinkedIn, companion repo).
- [ ] Clean up commit-message hygiene going forward (history has `test`, `fix merge`).
- [ ] `docs/production_extension.md`: drop the "when LatamGPT is available" framing — it
      launched Feb 2026 and is on Hugging Face now.

## P5 — Portfolio

- [ ] Cross-link with `latam-rag-quality-gate`.
- [ ] Consider a flagship integration repo: LatamGPT vs frontier models on a real LATAM eval
      set, run through this Lakehouse pipeline with the quality gate inline.
- [ ] "Evaluating and gating LatamGPT for regional Spanish" writeup (Medium + podcast).
