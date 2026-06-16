# Changelog

All notable changes to the Operating Principles spec are recorded here. The project is **pre-1.0** until the first stable public release. While `0.x`, minor versions may still reshape obligations and downstream implementations must re-check conformance; patch versions are clarifications/fixes.

This repo uses **Release Please** for managed release PRs, changelog maintenance, and tags going forward.

## 0.3.0 — 2026-06-16

Incorporated the approved domain-principles proposal and moved backlog tracking into the repo-local Beads instance.

### Added
- **Top-level Integrity floor** — honesty, non-maleficence, transparency about uncertainty/limits, and accountability as non-negotiable constraints under all optimization.
- **Principles as decision algorithms** — principles should be usable before decisions, debated, revised, versioned, and improved by reflective learning.
- **Standard #12 Probabilistic judgment & calibration** — beliefs carry odds; base rates, reference classes, confidence calibration, and decision-process review.
- **Standard #13 Execution right-sizing** — match workflow/agent/model/effort to task structure and stakes; outcome-first direction for delegation.
- **Domain principles: Knowledge & learning** — atomic durable notes, retrieval practice, deliberate practice, hierarchy plus links.
- **Domain principles: AI agent operations** — harness as product, context-loading discipline, trigger/recurrence design, mutation safety pre-flight.
- **Domain principles: Human agency & ethics** — informed consent, conflicts of interest, transparency/accountability for consequential human-affecting work.
- **Endnotes** — complete citation entries for newly incorporated and backlog sources.
- **Repo-local Beads backlog** — domain-mining backlog now lives in Beads epic `op-q95`, not committed markdown lists.
- **Release Please configuration** — lightweight managed release process for this repo.

### Expanded
- **System optimization** — added delays/oscillation, ranked leverage points, requisite variety, purpose-from-behavior, and compound engineering / system-that-produces-the-work.
- **Documentation** — added write-to-think.
- **Reuse & simplicity** — sharpened locality of override.
- **Streamlined maintenance** — named the PDCA loop and “convert repeated fixes into standards.”
- **Foundations** — added Ray Dalio's *Principles*, behavioral psychology/cognitive-bias sources, and Anthropic workflow/agent guidance.

### Changed
- Version tracking revised from premature `1.x` to pre-1.0 `0.x`.
- Proposal/backlog review flow moves to pull requests plus Beads, rather than committed proposal files as the durable backlog.

## 0.2.0 — 2026-06-14

Formerly labeled `1.1.0`. Reconciled principles from parallel codification attempts (a security-workspace constitution, a plugin-system constitution, and a machine-readable preference doc) and added the domain-examination method.

### Added
- **Standard #10 Version-aware state** — persisted state carries version metadata; semver + ISO 8601.
- **Standard #11 Time-boxed exploration** — explicit time box before exploratory work; continue/park/discard at the limit.
- **Hard vs. soft rules** in the conformance model — hard rules are never violable (the safety/honesty floor); soft rules are strong defaults that may yield with a stated reason.
- **How this spec grows** — a repeatable domain-examination method.

### Expanded
- **#2 Issue management** — added *capture before clarity* (speed of capture > quality; refine later). Foundation: GTD.
- **#3 Verification & Validation** — added intentional review-gate design and the *trust-graduates-on-evidence* autonomy ratchet.
- **#12 Reuse & simplicity** — added *hierarchy-first / one home per fact*.
- **#16 Audience-tailoring** — added the *graduated output quality* tier table.
- Foundations table: added GTD, progressive-autonomy/trust-tier practice, semantic-versioning/schema-migration.

## 0.1.0 — 2026-06-14

Formerly labeled `1.0.0`. First versioned publication as a standalone, substrate-independent specification and source of record.

### Top-level
- System optimization — improve the whole, not one piece.

### Core standards
- Specifications — contract before build, with the spec-vs-prose decision rule.
- Issue management — one visible source of truth for work.
- Verification & Validation — prove it's right and right-for-purpose; execute, don't assert; adversarial critique before presenting; intentional review-gate design.

### Operational standards
- Commit conventions — atomic, conventional commits.
- Secret hygiene — no plaintext secrets, fail closed, never print.
- File layout — predictable, discoverable locations (XDG).
- Session closeout — work isn't done until it's shipped AND shared; sharing is a deliberate habit, informal by default.
- Output hygiene — no internal identifiers across a trust boundary.
- Documentation — required for any development effort, refreshed with the code.

### Design principles
- Reuse & simplicity — prefer existing tools; simplest sufficient solution.
- Streamlined maintenance — automate the chore; watchdog pattern.
- Reliability & resilience — fail safe, degrade gracefully, recover fast.
- Fast feedback / small reversible changes — small, safe, frequent beats big, infrequent.

### Communication standards
- Audience-tailoring — audience is a mandatory input; brevity wins.
- Writing-style — match the author's voice, getting more precise over time.

### Domain principles
- Security — Rick Howard's Cybersecurity First Principles.

### Framing
- Established as the **harness for everything else**, including coding-agent harnesses.
- Substrate-independent source of record; implementations are downstream projections that conform to it.
- Conformance language and semantic versioning introduced.
