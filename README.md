# Jailbreak Robustness Eval Harness

> A reproducible harness for scoring LLM refusal robustness against public
> harmful-prompt benchmarks, with validated judging and benign over-refusal tracking.
>
> **Status:** 🟡 Scaffolding — in progress. Results below are placeholders.

Part of a small portfolio of empirical AI safety & security studies:
- **P1 — Jailbreak eval harness** *(this repo)*
- P2 — Rapid-response jailbreak defense (reproduction)
- P3 — Agentic tool-use injection study (AgentDojo)

---

## Motivation

Published jailbreak results are frequently overstated — automated evaluators tend to
overestimate attack success, and "robustness" claims often omit the cost side
(legitimate prompts wrongly refused). This project builds a clean, honest measurement
layer: given a model and a public benchmark, what is its attack-success-rate per harm
category, and what does robustness cost in benign over-refusal?

This is foundational empirical-ML work — reproducible evaluation done carefully — rather
than a novel method. The deliverable is a harness others can trust and extend.

## What this measures

- **Attack-success-rate (ASR)** and **refusal-rate**, per harm category, per model
- **Benign over-refusal rate (FPR)** on a held-out benign split
- **Judge–human agreement** on a hand-labeled sample (the harness validates its own judge)

## Data & tooling

- **JailbreakBench (JBB-Behaviors)** — primary dataset (100 behaviors + benign set), MIT.
  `huggingface.co/datasets/JailbreakBench/JBB-Behaviors`
- Optional second dataset: **HarmBench** behaviors for a generalization check.
- Model access via **LiteLLM** (API) and/or local small open-weights models.

## Setup

```bash
python -m venv .venv && source .venv/bin/activate
pip install -U pip
pip install datasets transformers pandas numpy scikit-learn matplotlib tqdm litellm
# dataset/judge helpers
pip install jailbreakbench
```

## Reproduce

```bash
# placeholder — wire up once scaffolding lands
# python -m harness.run --models config/models.yaml --dataset jbb --out runs/
# python -m harness.judge --run runs/<id> --validate-sample 50
# python -m harness.report --run runs/<id>
```

All model/provider/version choices live in `config/` and are logged with every run.

## Results

> _To be filled in. Template below._

| Model | ASR ↓ | Refusal ↑ | Benign over-refusal ↓ | Judge agreement |
|---|---|---|---|---|
| _model A_ | — | — | — | — |
| _model B_ | — | — | — | — |

**Judge validation:** hand-labeled _n_ = TBD; agreement = TBD. Notes on disagreements: TBD.

## Responsible use

Uses existing public benchmarks under their licenses. Reports aggregate rates only;
does not publish novel working harmful payloads. Some benchmark prompts are offensive by
design — handle accordingly.

## Roadmap

- [ ] Dataset loader (harmful + benign splits)
- [ ] Target runner via LiteLLM, with run metadata persisted
- [ ] Rule-based refusal detector (baseline judge)
- [ ] Model-based judge + hand-labeled validation subset
- [ ] Per-category metrics + benign FPR
- [ ] Cross-model report + writeup
- [ ] `make reproduce` one-command path

## References

- Chao et al., *JailbreakBench* (NeurIPS 2024 D&B) — `github.com/JailbreakBench/jailbreakbench`
- Mazeika et al., *HarmBench* — `github.com/centerforaisafety/HarmBench`

## License

Code: TBD. Benchmark data remains under its original license (JBB-Behaviors: MIT).
