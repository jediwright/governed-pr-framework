<!--
PR Template · Governed PR Framework v0.3 (J. Wright — see LINEAGE.md for design notes; optional reading)
New here? Read QUICKSTART.md first — 90 seconds, and it's all you need.

HOW THIS WORKS
1. Declare your tier below. 2. Fill only the sections your tier requires. 3. Delete unused sections.
Tier disputes resolve UPWARD (reviewer's call wins if higher).
Changes touching a protected surface (see CONTRIBUTING.md) are automatically Critical.
Changes matching a pre-cleared class (see CONTRIBUTING.md) are Low-risk: name the class
as your intent line; the automated class-membership gate and green CI are the only requirements.
This repo's review scale is set in CONTRIBUTING.md — you don't declare it here.

EMERGENCY CHANGES (live incidents, security responses): act first, then open this PR
retrospectively within the declared window. Fill it as a Critical-tier PR with honest
after-the-fact tags. See §10.1 of the framework for the full procedure.
-->

## Change Tier
<!-- Pick ONE. Tier = how far a failure would spread, not how many lines changed.
     Low-risk  — failure would be local and visible (rename, constant fix, test-only change)
     Feature   — failure could spread within one area (new feature, module refactor)
     Critical  — failure could be silent or unrecoverable (schema, sync, permissions,
                 dependencies, deploy config, deleting code) -->

**Tier:** Low-risk / Feature / Critical

---

## Intent
<!-- ALL TIERS. What this changes and why — readable without opening the diff.
     Example: "Fixes the cart total showing $0 after page reload by re-attaching the
     observer when the document rehydrates from storage." -->



<!-- ============ LOW-RISK PRs STOP HERE. Everything below is Feature tier and up. ============ -->

## Acceptance Criteria  <!-- Feature + Critical -->
<!-- Written BEFORE the code. Given / when / then. Point each one at where it's met.
     Example: "Given a saved cart, when the page reloads, then the total matches the
     line items → met in useCart.ts re-attach logic + cart.reload.test.ts" -->

- [ ] Given … when … then … → met in: …
- [ ] Given … when … then … → met in: …

## Verification Status  <!-- Feature + Critical -->
<!-- Tag each substantive claim in this PR. The tags:
     Confirmed      — verified; say against WHAT (test run, dependency version) and when
     Inferred       — follows from something confirmed; state the reasoning
     Unverified     — assumed; MUST include a closure plan (what you'll watch, by when).
                      Not allowed at all on protected surfaces.
     Time-sensitive — true now; name what will make it expire -->

| Claim | Tag | Evidence / reasoning / closure plan |
|---|---|---|
| Reload no longer drops the total | Confirmed | 31/31 tests passing, run linked, 2026-08-06, against lib v2.6.0 |
| No other views read this observer | Inferred | grep shows single consumer; reasoning in thread |

## Not in this PR
<!-- One line. What you deliberately left out, and why leaving it out is safe.
     Example: "Not in this PR: multi-tab sync — safe to defer because single-tab
     behavior is unchanged and multi-tab is flagged off." -->

**Not in this PR:** … — **safe to defer because:** …

## Pre-mortem  <!-- Feature + Critical -->
<!-- Answer in writing: "It's two weeks from now and this PR caused an incident.
     What was it?" This catches what checklists can't. -->



<!-- ============ FEATURE PRs STOP HERE. Everything below is Critical tier only. ============ -->

## Convention Check  <!-- Critical -->
<!-- Link the doc that governs any data convention / key format / protocol / schema you touched.
     If no doc exists yet: writing it is part of this PR. Code and convention ship together. -->

- Convention doc(s):
- New/updated doc included in this PR (if a gap was found):

## Decision Record  <!-- Critical — only if this PR settles a question that would fail silently if wrong -->
<!-- Link a short record: context / decision / alternatives considered / consequences.
     Ordinary implementation choices that a later refactor could visibly reverse don't need one. -->

- Decision record link:

## Boundary Questions  <!-- Critical — protected surfaces only -->
<!-- Does this change what any party can SEE, FORGE, REPLAY, or DENY?
     "No change" is a fine answer. A blank is not. -->

- See:
- Forge:
- Replay:
- Deny:

## Deletion Justification  <!-- Critical — only if code is removed -->
<!-- Why did the removed code exist? If nobody knows, that's a documentation gap to log —
     not permission to delete. -->



## Verification Chain  <!-- Critical — bug fixes only -->
<!-- "Fixed the bug" isn't evidence. Show the trail. -->

- Symptom (precise):
- Root cause (confirmed, not guessed):
- How it was confirmed (hypothesis → minimal test → result):

---

## Review  <!-- completed by the reviewer, not the author -->

- **Tier declaration matches the diff:** <!-- yes | disputed → resolves upward -->
- **Reviewed outside the authoring context via:** <!-- second person | separate session vs. spec (solo repos) -->
- **Automated checks:** <!-- green | bypass declared above with reason -->
- **No Unverified tags on protected surfaces:** <!-- confirmed | n/a -->

**Reviewer scope** <!-- required on Feature+ in org-scale repos; see CONTRIBUTING.md -->
- Approved (what I evaluated):
- Not evaluated (outside my domain):

**Block note** <!-- anyone may block any PR; overriding a block requires written justification here, whoever blocked -->

---
<!-- Before merging, remember:
     · Rebased across a dependency bump? Confirmed tags on affected claims are stale — re-verify.
     · PR open past the staleness window (default 14 days)? Re-verify Confirmed tags; don't just rebase. -->
