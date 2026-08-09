# GPRF Vocabulary — v0.4

**Namespace IRI:** `https://jediwright.github.io/governed-pr-framework/vocab/gprf/0.4#`

**Framework:** [Governed PR Framework](https://github.com/jediwright/governed-pr-framework)
**Date declared:** 2026-08-09

---

## About this namespace

This namespace declares the machine-readable vocabulary for the Governed PR
Framework (GPRF) v0.4. GPRF v0.3 and earlier defined its verification-tag
system as prose and template convention — the four-tag set (Confirmed /
Inferred / Unverified / Time-sensitive), K1–K4, the tier system, and the
reviewer-completed Review section. No machine vocabulary existed prior to v0.4.

This namespace formalizes GPRF v0.3's prose concepts as a
`seam:CrossingRecord` instance extension, following the alias-mapping
amendment of 2026-08-09.

---

## Vocabulary terms

### `gprf:VerificationRecord`

A `seam:CrossingRecord` instance extension representing a GPRF-verified
pull request merge. Reviewer identity is carried by the base field
`seam:emittedBy` (no instance-level `reviewerDID` exists — collapsed per
GPRF v0.4 alias-mapping amendment, 2026-08-09). Record timestamp is
carried by the base field `seam:emittedAt` (no instance-level
`verificationTimestamp` exists — no dual-emission transition applies;
verified absent at declaration time).

### `gprf:prReference`

**Type:** URI
**Requirement:** Required
**Description:** The pull request being verified.

### `gprf:blastRadiusClass`

**Type:** Controlled vocabulary
**Requirement:** Required
**Values:**

| Value | Description |
|---|---|
| `low-risk` | Changes where failure is local and visible; no protected surface touched. |
| `feature` | Changes introducing new behavior; blast radius extends to dependent surfaces. |
| `critical` | Changes touching protected surfaces (`types.ts`, `gate.ts`, schema declarations, or equivalent). Automatic tier for protected-surface changes; not discretionary. |

### `gprf:verificationOutcome`

**Type:** Controlled vocabulary
**Requirement:** Required
**Values:**

| Value | Description |
|---|---|
| `approved` | Change verified against its blast-radius classification; all K1–K4 requirements satisfied. |
| `approved-with-conditions` | Approved subject to named conditions; conditions stated in the Review section. |
| `blocked` | Change does not satisfy admissibility requirements; specific finding stated in the Review section. |

---

## Alias mapping (v0.4)

| Concept | GPRF v0.3 prose surface | v0.4 machine field |
|---|---|---|
| Reviewer identity | Reviewer name in PR template Review section | `seam:emittedBy` (base field) |
| Record timestamp | PR merge timestamp (implicit) | `seam:emittedAt` (base field) |
| PR reference | PR URL in template | `gprf:prReference` |
| Blast-radius tier | Change Tier (T1/T2/T3) | `gprf:blastRadiusClass` |
| Review outcome | Verification tag (Confirmed / Inferred / Unverified / Time-sensitive) | `gprf:verificationOutcome` |

---

## Governing documents

- `FRAMEWORK.md` — parent framework (prose)
- `gprf-v0-4-alias-mapping-amendment-note_2026-08-09.md` — alias-mapping
  session; §0 premise correction; Q1 and Q2 dispositions

---

**Status:** v0.4 — active development
**Specification:** [GPRF v0.4 alias-mapping amendment note, 2026-08-09](https://github.com/jediwright/governed-pr-framework)
**Maintainer:** [Jedi Wright](https://www.jediwright.com/) / [Systems of Thought](https://www.systemsofthought.com/) / [UX Minds, LLC](https://www.uxminds.org/)
