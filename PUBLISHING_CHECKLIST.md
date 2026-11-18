# Safe publishing checklist

This packet intentionally contains only high-level research writeups and aggregate CSV tables. Check all content before publishing publicly.

- [ ] Check that the GitHub repository's **Public/Private** visibility is what you intend.
- [ ] Confirm the local folder contains no model checkpoints, datasets, private source mappings, reviewer forms, private generated story text, or credentials.
- [ ] Read `git status --short` and `git diff --cached --stat` before committing.
- [ ] Only publish human-quality results after reviewer independence is no longer at risk.
- [ ] Do not imply that a provisional AI-only quality assessment is a confirmed quality improvement.

Upload only the extracted contents of this package, from a **new Git working directory**, rather than running `git add .` in the original NCM model repository.
