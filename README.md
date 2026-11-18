# ANGKON — CPU-Only Next-Concept Modeling R&D

**Independent exploratory research** on [HazyResearch Next-Concept Modeling (NCM)](https://github.com/HazyResearch/ncm), evaluated on TinyStories with frozen pretrained checkpoints in a Windows CPU-only environment.

> **Status: 18 November 2026.** This is a research log, not a claim of a new trained model or a demonstrated production improvement. This repository intentionally includes **only shareable summaries and aggregate measurements**. The independent human quality-review packets, reviewer identities, anonymization/deblinding keys, and provisional AI ratings remain unpublished while the reviews are pending.

## Research question

Can NCM's parallel coarse-to-fine concept generation retain its CPU generation advantage while improving the **logical coherence, entity consistency, and completeness** of short generated stories?

## Earlier exploratory milestones

- Phase 1 (AI-only TinyStories ratings): NCM **2.067/5** versus AR **4.083/5** (20 stories per model; provisional).
- Phase 2 (one CPU workstation): median generation-core throughput **6.81×** AR at batch 1 and **4.15×** AR at batch 4; this excludes selection/decoder overhead.
- Phase 3A: frozen VQ encode/decode achieved **99.9843%** native-token position agreement on 100 AR-generated references.
- Phase 3H: generated-prefix lock through L7 gave **94.73%** token-position agreement in a smaller precursor study.

See [`docs/research_history_phases_1_to_3.md`](docs/research_history_phases_1_to_3.md) for qualifications and provenance.

## Experiment snapshot

- Frozen VQ-VAE tokenizer: **36.43M** parameters; frozen NCP transformer: **88.61M** parameters (roughly **125M** combined).
- Native VQ-VAE output window: **128 token positions**.
- Hierarchical concept representation: **12 levels**, widths `1, 8, 16, 24, 32, 40, 52, 64, 76, 92, 108, 128`, totaling **641 concept-code positions**.
- Phase 4B: **30 independently generated base stories**, **2 suffix variants at each cutoff**, generated-prefix locks `L0, L3, L4, L5, L6, L7`, plus full-lock `L11` controls. **360** noncontrol suffix variants; **30** L11 controls.
- The suffix-resampling experiment resamples **all levels after cutoff K**, not only one level or only L4–L7.

## Confirmed technical observations

| Locked prefix | Locked code positions | Mean native token-position agreement |
|---|---:|---:|
| L0 | 1 | 6.64% |
| L3 | 49 | 31.65% |
| L4 | 81 | 52.25% |
| L5 | 121 | 69.64% |
| L6 | 173 | 84.65% |
| L7 | 237 | 93.75% |
| L11 (full lock/control) | 641 | 100.00% |

This supports the observation that coarse/mid-level concept prefixes strongly constrain decoded text. It **does not show** that those levels cause narrative defects or that resampling improves quality.

**Ending audit:** 2/30 base stories and 36/360 resampled stories ended with sentence-ending punctuation under an audit that permits trailing closing quotes. Punctuation is **not** semantic completion or an EOS measurement.

**Native EOS probe:** On the original user's frozen VQ-VAE, re-decoding all **30 base + 360 noncontrol variant** concept-code sequences reproduced **390/390** saved texts exactly; native EOS was present in **1/390** sequences. Native EOS ID was `0` and PAD ID `1`. This directly indicates that native EOS was rarely predicted by the decoder argmax within the 128-position window. It does **not** establish whether EOS was present in VQ-VAE training data or whether a longer native window would solve the ending issue.

## Repository contents

- [`docs/research_history_phases_1_to_3.md`](docs/research_history_phases_1_to_3.md) — earlier CPU benchmarking and diagnostics (reported historical results).
- [`docs/methodology.md`](docs/methodology.md) — experiment design and safeguards.
- [`docs/findings_and_limitations.md`](docs/findings_and_limitations.md) — interpretations, caveats, and status.
- [`results/phase4b/stability_by_cutoff.csv`](results/phase4b/stability_by_cutoff.csv) — aggregated generated-prefix stability measurements.
- [`results/phase4b/ending_by_cutoff.csv`](results/phase4b/ending_by_cutoff.csv) — aggregated text-ending measurements.
- [`results/phase4b/native_eos_by_group.csv`](results/phase4b/native_eos_by_group.csv) — EOS/PAD probe outcome reported by the CPU workstation.

## Research status

- Completed: Phase 3H/4B generated-prefix stability; Phase 4B read-only ending audit; frozen VQ-VAE native EOS probe.
- Pending: independent human review of Phase 4A and Phase 4B story quality.
- Not yet demonstrated: a reliable quality uplift from suffix resampling, trained intervention, CPU end-to-end speed advantage **after** a quality-selection overhead, or a causal explanation of missing EOS.

## Attribution and scope

NCM and pretrained checkpoints originate from the upstream HazyResearch project. ANGKON is an **independent CPU-only evaluation and investigation**, not the upstream model authorship. No upstream source code or weights are redistributed in this publication packet. Consult the upstream repository for its license and model usage requirements.

**Source of numbers:** author's local Windows CPU logs and user-supplied Phase 4B JSON, independently summarized into the aggregate CSVs. Analysis date: 2026-11-18. Generated-output JSON, complete source texts, and private review materials are deliberately not included.
