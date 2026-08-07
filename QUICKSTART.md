# Quick Start: Submitting a PR Here

*90 seconds. This is all you need to submit a correct PR. Everything else is optional depth.*

---

## 1. Pick your tier — by blast radius, not line count

Ask one question: **if this change were wrong, how far would the failure spread?**

| If a failure would be… | Your tier is | You fill in |
|---|---|---|
| Local and visible (a rename, a constant, a test-only change) | **Low-risk** | One line of intent. Done. |
| Contained to one area (a new feature, a module refactor) | **Feature** | Intent, acceptance criteria, verification tags, what you left out, one pre-mortem question |
| Silent or unrecoverable (schema, sync, permissions, dependencies, deploy config, deleting code) | **Critical** | Everything above, plus the Critical sections in the template |

Not sure? Pick the higher tier. If your reviewer disagrees with your pick, the higher of the two opinions wins — no debate needed.

Anything touching this repo's **protected surfaces** (listed in CONTRIBUTING.md) is automatically Critical, no matter how small the diff.

Going the other way: if your change matches a **pre-cleared class** listed in CONTRIBUTING.md, the automated class-membership gate and green CI are all you need — name the class as your intent line and you're done.

## 2. Tag your claims honestly

For Feature and Critical PRs, each substantive claim gets one tag:

- **Confirmed** — you verified it; say against what, and when
- **Inferred** — it follows from something confirmed; say how
- **Unverified** — you're assuming it; say what you'll watch after merge to find out (required — an assumption with no follow-up plan blocks the merge, and assumptions aren't allowed at all on protected surfaces)
- **Time-sensitive** — true today; say what will make it stop being true

Honest "Unverified" beats confident silence. The tags exist so your reviewer knows what they're inheriting versus what they need to check themselves.

## 3. Answer the pre-mortem (Feature and Critical)

One question, answered in writing: *"It's two weeks from now and this PR caused an incident — what was it?"* Thirty seconds of imagination catches what checklists can't.

## 4. What your reviewer will check first

1. Does your tier pick match the diff? (This is check #1, always.)
2. Was this reviewed by someone — or some context — other than what wrote it?
3. Are the automated checks green?
4. Any Unverified tags on protected surfaces? (Automatic no.)

## Two things that surprise people

- **Small ≠ Low-risk.** A one-line schema change is Critical. A 300-line test file is Low-risk. Tier is about propagation.
- **If your PR revealed something undocumented** — a convention nobody wrote down, a failure mode not on the list — updating that doc is part of your PR. Code and documentation ship together.

## If it's an emergency

Live incident, security response, something that can't wait for review? **Act first.** Apply the fix. Then open a PR retrospectively within this repository's declared window and fill it as a Critical-tier PR with honest after-the-fact tags — "Confirmed" still means verified; "Unverified" still needs a closure plan. The emergency path moves the governance, it doesn't remove it. See §10.1 of the framework for the full procedure.

---

*That's it. Full rules: the framework document. Why it's built this way: `LINEAGE.md`. Neither is required reading.*

*Based on the Governed PR Framework v0.3 by J. Wright.*
