# Methodology — generated-prefix stability (Phase 4B)

## Source and provenance

Author's generated-prefix diagnostic, run on the pretrained/frozen NCM components on a Windows CPU-only machine. The source Phase 4B JSON SHA-256 was:

`7934671292eaa6ccc91b0058a05eb29b866ab85a7998fa85504b4980321ab1a1`

The detailed JSON is retained privately. This public repository contains only aggregate tables.

## Design

- Start with 30 independently generated base stories, using checkpoint-sampled level-0 and NCP-generated later codes (not reference-oracle prefixes).
- For each base story and cutoff K in `0, 3, 4, 5, 6, 7`, retain generated codes from levels 0 through K and resample **all** higher levels with independent draws at temperature 1.0, 2 suffix variants per cutoff.
- Full code lock `L11` supplies an exact-reproduction control.
- Code level widths `1,8,16,24,32,40,52,64,76,92,108,128` sum to 641 concept positions.
- Text has a fixed 128-position VQ-VAE native decoding window.

## Evaluation

1. Native-token-position agreement compares resampled decoded text against the base story at corresponding token positions; text shifts can lower this measure.
2. Character similarity and word-bigram Jaccard measure surface-form similarity; they **do not measure story coherence**.
3. Percentage of changed suffix codes captures latent perturbation relative to the base.
4. Text-ending proxies count punctuation after stripping whitespace and permitting final quotation marks; these do **not** measure EOS or narrative closure.
5. A separate on-device probe used the *frozen* VQ-VAE to reconstruct native token IDs and check EOS/PAD; exact text reproduction was verified for all 390 noncontrol evaluated texts.

## Sampling caveats

- The 2 variants from the same base story are correlated. Do not treat 360 variants as 360 independent stories.
- Different cutoffs should not be compared for story-quality improvement without matched cross-cutoff quality assessments.
- No new fine-tuning or reranker was evaluated in these technical diagnostics.
- Do not infer that fixed-length token generation is the sole cause of abrupt endings.
- Private blinded human reviews remain pending and are purposefully excluded from public materials.
