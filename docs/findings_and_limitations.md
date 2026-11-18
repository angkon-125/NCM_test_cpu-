# Findings, limitations, and next steps

## Finding 1 — concept-prefix stability

The output is highly stable when codes through level L7 are frozen (mean 93.75% token-position agreement), although mean changed *suffix* code percentage is about 50.12%. Stable output is **not** proof of a coherent or correct story.

## Finding 2 — incomplete endings are prevalent

The text-formatting audit found sentence-ending punctuation in 2 of 30 base stories and 36 of 360 suffix variants. These counts include punctuation followed by a closing quotation mark; a strict final-character-only rule yields different counts. Treat both as **mechanical proxies**, not semantic closure.

## Finding 3 — native EOS is almost always absent

A frozen VQ-VAE-only probe on the author's Windows CPU machine re-decoded 390 saved code sequences: 30 base stories and 360 resampled variants. The resulting text matched all recorded texts exactly. EOS was predicted somewhere in the native 128-position argmax window for just 1/390 sequences; no PAD-before-EOS case was reported. The encoder's behavior on two independent complete example sentences also did not automatically append EOS. **This does not prove EOS was absent from original training targets.**

## Unresolved questions

1. How often did EOS actually occur in the VQ-VAE's tokenized **training targets**?
2. Is the absence of EOS a consequence of fixed-length training blocks, reconstruction targets, loss weighting, or the distribution of NCP-generated concept codes?
3. Does any intervention improve independently evaluated plot logic/entity consistency, rather than only similarity or punctuation?
4. Does a quality improvement preserve CPU end-to-end performance once intervention overhead is included?

## Safeguards

Keep all checkpoints frozen until there is a controlled, justified intervention. Do not interpret AI-only, provisional story reviews as independent human evidence. Do not publish reviewer score sheets, anonymization keys, or deblinded per-pair analyses while human reviews remain underway.
