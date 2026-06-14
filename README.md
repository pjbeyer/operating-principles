# Operating Principles

The canonical specification for how I want my entire system of work to operate.

This repository is the **source of record**. It is not documentation about a tool — it is the spec that tools, devices, services, apps, agents, and even employment positions are expected to **conform to**. It is deliberately substrate-independent: it does not belong to any coding agent, project repo, online service, or workstation.

**It is the harness for everything else — including coding-agent harnesses.** A coding-agent harness (Hermes, Claude Code, an IDE assistant, a CI bot) sits *inside* this spec, not beside it. This is the outermost layer that wraps and governs every harness, tool, and workflow beneath it. When a harness defines its own rules, those rules implement this spec — not the other way around. It's the harness that holds the harnesses.

## What's here

- **[`PRINCIPLES.md`](./PRINCIPLES.md)** — the specification itself: a top-level principle, core / operational / design / communication standards, and domain principles (e.g. security), each derived from a well-established framework and synthesized into one coherent, opinionated set.
- **[`CHANGELOG.md`](./CHANGELOG.md)** — versioned history of the spec.

## How it's used

Implementations are **downstream projections** of this spec. Wherever the content also lives — a coding agent's skills, a workstation's dotfiles, a project's `AGENTS.md`, a service's configuration — that copy *implements* the spec and conforms to it. When the spec and an implementation disagree, the spec wins and the implementation is updated to match. An implementation should be able to declare which spec version it implements, so drift stays visible.

## Versioning

Semantic versioning of the spec:

- **MAJOR** — a breaking change to a standard's meaning, or a removal (implementations must re-check conformance).
- **MINOR** — a new standard or a materially expanded one (backward-compatible).
- **PATCH** — wording/clarification with no change in obligation.

The current version is stated at the top of `PRINCIPLES.md`; changes are recorded in `CHANGELOG.md`.

## License

[MIT](./LICENSE) — reuse freely.
