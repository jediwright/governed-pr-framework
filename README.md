# The Governed Pull Request Framework

A lightweight PR framework that scales review rigor by **blast radius, not line count** — and requires every claim in a PR to be either verified or honestly tagged as not yet verified.

The framework enforces three properties through every PR: **Clarity** (the reviewer reads intent off the description, not out of the diff), **Consistency** (the bar does not move with deadline pressure, author, or reviewer), and **Credibility** (no claim passes untagged).

**v0.4** — alias mapping amendment applied (GPRF vocabulary namespace live); in use at [UX Minds, LLC](https://www.jediwright.com).

---

## What's here

| File | What it is |
|---|---|
| `QUICKSTART.md` | 90 seconds. Everything a contributor needs to submit a correct PR. Start here. |
| `.github/PULL_REQUEST_TEMPLATE.md` | The PR template — auto-populated by GitHub when you open a PR in any repo that adopts this. |
| `FRAMEWORK.md` | The full framework: tier definitions, verification tag rules, scale gates, measurement, emergency path, inheritance model. For reviewers, adopters, and maintainers. |
| `LINEAGE.md` | Design rationale and term origins — why the framework is built the way it is. Optional context; nothing in the PR process depends on it. |

---

## Adopting this framework

This document is the **parent**. To use it in your repo:

1. Copy `QUICKSTART.md` and `.github/PULL_REQUEST_TEMPLATE.md` into your repo as-is.
2. Create a `CONTRIBUTING.md` that declares your repo's protected surfaces, pre-cleared change classes, operating scale, and (if different from the 1 business day default) your emergency change window. `FRAMEWORK.md` §2–§3 defines what each of those means.
3. Carry a one-line attribution back to this repo. `LINEAGE.md` does not ship with derivatives.

Derivative-local customizations never flow back upstream. If you discover an improvement that belongs in the parent, open a PR here.

---

## In use

| Repo | Adopted | Notes |
| ---- | ------- | ----- |
| [`employment-seam`](https://github.com/jediwright/employment-seam) | v0.3 | First derivative deployment; `CONTRIBUTING.md` + PR template adopted from v0.3; GPRF vocabulary (`gprf:verificationTag`) in active use via `seam:CrossingRecord` base shape (v0.4) |

---

## The two things that surprise people

- **Small ≠ Low-risk.** A one-line schema change is Critical. A 300-line test file is Low-risk. Tier is about how far a failure would spread, not how much work went in.
- **"Unverified" is not a failure.** It is the honest tag for an assumption. What blocks a merge is an assumption with no closure plan — not the assumption itself.

---

*J. Wright · [UX Minds, LLC](https://www.jediwright.com) · AI-assisted (Claude / Anthropic)*
