# Research record — Phases 1–3 (historical context)

These values were reported in the project handoff prepared **18 November 2026** (`Angkon_NCM_RnD_Handoff_2026-11-18`). They are **historical exploratory results**, not freshly reproduced from raw experiment files in this public packet. Underlying model files, original scored text, and raw benchmarks have not been published here.

| Phase | Reported measurement | Interpretation and limitation |
|---|---|---|
| Phase 1: TinyStories quality | NCM **2.067/5** vs. AR **4.083/5**, based on 20 AI-reviewed stories per model | AI subjective scoring, not independent human review; models are not controlled training-matched ablations |
| Phase 2: CPU throughput, batch 1 | NCM **168.20** vs. AR **24.70** GPT-2-equivalent tokens/s (**6.81×**) | Median generation-core throughput on one CPU; excludes model loading, text decoding, and quality-selection overhead |
| Phase 2: CPU throughput, batch 4 | NCM **233.55** vs. AR **56.21** tokens/s (**4.15×**) | Higher throughput but higher NCM working-set memory; not generalizable to other hardware |
| Phase 3A: frozen VQ reconstruction | **99.9843%** native-token agreement on 100 AR-generated reference stories | Strong reconstructions for encoded references, not proof generated code combinations are equally valid |
| Phase 3B: marginal code use | No clear marginal codebook collapse in a small 20-story comparison | Does not measure cross-level dependencies or meaning |
| Phase 3C: teacher-forced NCP | **62.695%** position-weighted top-1 across 12,800 code labels | True previous levels are provided, so error accumulation is not measured |
| Phase 3E: reference-oracle prefix recovery | L4 **76.37%**, L5 **88.83%**, L7 **98.48%** token agreement | A *reference-oracle* diagnostic; not achievable when sampling free-running generated prefixes |
| Phase 3G: decoding temperatures | AI-rated quality ~**2.16–2.27/5** in the reported replication | Small uncertain changes; not a validated intervention |
| Phase 3H: generated-prefix stability | Lock through L7: **94.73%** token agreement while **50.88%** of suffix codes differed | Confirms stability of text under resampling, not semantic correctness |

## Phase 4: latest evidence

The Phase 4B study in this repository extends Phase 3H to 30 base stories with two resampled continuations at each noncontrol cutoff; see the primary [`README.md`](../README.md) and aggregate CSV tables. Blind story-quality evaluations are underway and **not published** in this public starter pack.

## Scientific caution

Do not compare all reported quality scales as if identical. Phase 1, Phase 3, and Phase 4 pilot assessments used different review designs and in some cases different rubric categories. Throughput is *not* end-to-end latency; it cannot establish whether a subsequent multi-sample reranker preserves CPU advantage.
