# Changelog

All notable changes to the Operating Principles spec are recorded here. The spec follows semantic versioning (MAJOR = breaking change to a standard's meaning or a removal; MINOR = new/expanded standard, backward-compatible; PATCH = wording/clarification with no change in obligation).

## 1.0.0 — 2026-06-14

First versioned release as a standalone, substrate-independent specification and source of record.

### Top-level
- System optimization — improve the whole, not one piece.

### Core standards
- Specifications — contract before build, with the spec-vs-prose decision rule.
- Issue management — one visible source of truth for work.
- Verification & Validation — prove it's right and right-for-purpose; execute, don't assert; adversarial critique before presenting; intentional review-gate design (graduating vs always-gated).

### Operational standards
- Commit conventions — atomic, conventional commits.
- Secret hygiene — no plaintext secrets, fail closed, never print.
- File layout — predictable, discoverable locations (XDG).
- Session closeout — work isn't done until it's shipped AND shared; sharing is a deliberate habit, informal by default.
- Output hygiene — no internal identifiers across a trust boundary.
- Documentation — required for any development effort, refreshed with the code.

### Design principles
- Reuse & simplicity — prefer existing tools; simplest sufficient solution.
- Streamlined maintenance — automate the chore; watchdog pattern (folds in cost/efficiency and observability).
- Reliability & resilience — fail safe, degrade gracefully, recover fast.
- Fast feedback / small reversible changes — small, safe, frequent beats big, infrequent.

### Communication standards
- Audience-tailoring — audience is a mandatory input; brevity wins.
- Writing-style — match the author's voice, getting more precise over time.

### Domain principles
- Security — Rick Howard's Cybersecurity First Principles (reduce probability of material impact; Zero Trust, Intrusion Kill Chain Prevention, Resilience, Risk Forecasting, Automation).

### Framing
- Established as the **harness for everything else**, including coding-agent harnesses.
- Substrate-independent source of record; implementations (coding-agent skills, dotfiles, project `AGENTS.md`, service config) are downstream projections that conform to it.
- Conformance language and semantic versioning introduced.
