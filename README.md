# Operating Principles

The canonical specification for how I want my entire system of work to operate.

This repository is the **source of record**. It is not documentation about a tool — it is the spec that tools, devices, services, apps, agents, and even employment positions are expected to **conform to**. It is deliberately substrate-independent: it does not belong to any coding agent, project repo, online service, or workstation.

**It is the harness for everything else — including coding-agent harnesses.** A coding-agent harness (Hermes, Claude Code, an IDE assistant, a CI bot) sits *inside* this spec, not beside it. This is the outermost layer that wraps and governs every harness, tool, and workflow beneath it. When a harness defines its own rules, those rules implement this spec — not the other way around. It's the harness that holds the harnesses.

## What's here

- **[`PRINCIPLES.md`](./PRINCIPLES.md)** — the specification itself: top-level principles, core / operational / design / communication standards, domain principles, foundations, and endnote citations.
- **[`CHANGELOG.md`](./CHANGELOG.md)** — versioned history of the spec.
- **Repo-local Beads (`bd`)** — source of truth for domain-mining backlog and durable work; start with `bd prime` and `bd ready`.

## Status

This repo is **pre-1.0**. The current spec version is stated at the top of `PRINCIPLES.md`. The work is intentionally leading toward a stable v1 release; until then, `0.x` minor versions may still reshape obligations and downstream implementations should re-check conformance on each minor bump.

## How it's used

Implementations are **downstream projections** of this spec. Wherever the content also lives — a coding agent's skills, a workstation's dotfiles, a project's `AGENTS.md`, a service's configuration — that copy *implements* the spec and conforms to it. When the spec and an implementation disagree, the spec wins and the implementation is updated to match. An implementation should be able to declare which spec version it implements, so drift stays visible.

## Change process

- Use **pull requests** for reviewable spec changes, proposals, and process changes.
- Use **Beads** for the durable backlog; do not keep open backlog lists in committed markdown files.
- Attribute throughout: brief inline *Foundation* callouts in the spec body, plus complete citation entries as endnotes.
- Keep the spec substrate-independent: no private paths, internal tracker IDs outside this repo's own maintenance context, tool-internal mechanics, secrets, or workplace-private details.

## Releases

This repo uses **Release Please** as the lightweight managed release process.

- Conventional Commit messages drive Release Please's release PR.
- Release Please maintains changelog/tag state going forward.
- Manual edits to `CHANGELOG.md` are acceptable when curating pre-1.0 history, but future release entries should normally flow through Release Please.

## Versioning

Semantic versioning, in pre-1.0 form:

- **0.MINOR** — a new standard, materially expanded standard, or other obligation-shaping change. Downstream implementations must re-check conformance.
- **0.MINOR.PATCH** — wording/clarification/fix with no change in obligation.
- **1.0.0** — first stable public operating spec.

## License

[MIT](./LICENSE) — reuse freely.
