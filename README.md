# The Governed Pull Request Framework

A lightweight PR framework that scales review rigor by **blast radius, not line count** — and requires every claim in a PR to be either verified or honestly tagged as not yet verified.

The framework enforces three properties through every PR: **Clarity** (the reviewer reads intent off the description, not out of the diff), **Consistency** (the bar does not move with deadline pressure, author, or reviewer), and **Credibility** (no claim passes untagged).

**Version:** framework v0.3 (2026-08-06) · machine vocabulary v0.4 (2026-08-09). The framework text, quick start, and PR template are v0.3. The v0.4 release added only an optional machine-readable vocabulary (`vocab/gprf/0.4/`); nothing a contributor fills in changed. In use at UX Minds, LLC, as part of the [Seam Stack portfolio](https://github.com/jediwright/seam-stack/blob/main/BLUEPRINT.md).

---

## What's here

| File | What it is |
|---|---|
| `QUICKSTART.md` | 90 seconds. Everything a contributor needs to submit a correct PR. Start here. |
| `.github/PULL_REQUEST_TEMPLATE.md` | The PR template — auto-populated by GitHub when you open a PR in any repo that adopts this. |
| `FRAMEWORK.md` | The full framework: tier definitions, verification tag rules, scale gates, measurement, emergency path, inheritance model. For reviewers, adopters, and maintainers. |
| `LINEAGE.md` | Design rationale and term origins — why the framework is built the way it is. Optional context; nothing in the PR process depends on it. |
| `vocab/gprf/0.4/` | Machine-readable vocabulary for recording verified merges as structured data. Optional; in active development. Not needed to adopt the framework. |

---

## Adopting this framework

This document is the **parent**. To use it in your repo:

1. Copy `QUICKSTART.md` and `.github/PULL_REQUEST_TEMPLATE.md` into your repo as-is.
2. Create a `CONTRIBUTING.md` that declares your repo's protected surfaces, pre-cleared change classes, operating scale, and (if different from the 1 business day default) your emergency change window. `FRAMEWORK.md` §2–§3 defines what each of those means.
3. Keep the one-line attribution at the bottom of `QUICKSTART.md` (*"Based on the Governed PR Framework v0.3 by Jedi Wright."*) and link it to this repo. `LINEAGE.md` does not ship with derivatives.

Derivative-local customizations never flow back upstream. If you discover an improvement that belongs in the parent, open a PR here.

---

## In use

| Repo | Adopted | Notes |
| ---- | ------- | ----- |
| [`employment-seam`](https://github.com/jediwright/employment-seam) | framework v0.3 · vocabulary v0.4 | First derivative deployment; `CONTRIBUTING.md` + PR template adopted from v0.3; defines a GPRF verification record type in its crossing-record code (`keyhive-employment-seam/src/crossingRecord.ts`), following the v0.4 vocabulary |
| [`local-first-social-network`](https://github.com/jediwright/local-first-social-network) | framework v0.3 | `CONTRIBUTING.md` + PR template adopted as a governed derivative |
| [`local-first-social-native`](https://github.com/jediwright/local-first-social-native) | framework v0.3 | `.github/CONTRIBUTING.md` + PR template adopted as a governed derivative |

---

## The two things that surprise people

- **Small ≠ Low-risk.** A one-line schema change is Critical. A 300-line test file is Low-risk. Tier is about how far a failure would spread, not how much work went in.
- **"Unverified" is not a failure.** It is the honest tag for an assumption. What blocks a merge is an assumption with no closure plan — not the assumption itself.

---

## License

MIT. See [`LICENSE`](LICENSE).

---

*MIT License · Built with AI-collaborative methods · Intellectual direction and authorial responsibility: Jedi Wright · Systems of Thought · UX Minds, LLC*
