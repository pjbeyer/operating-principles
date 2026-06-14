# Phil's Operating Principles — a personal specification

**Spec version: 1.0.0** · Status: active · Canonical source of record (see *Status & canonical home* below)

This document is a **specification for how Phil's entire system of work should operate.** It is not documentation *about* a tool — it is the source specification that tools, devices, services, apps, agents, and even employment positions are expected to **conform to**. When Phil configures an AI agent, sets up a workstation, adopts a service, or evaluates a job, the question is: *does it operate the way this spec describes?*

It is deliberately **substrate-independent**. It is not tied to any coding agent, project repository, online service, or workstation. Those are all just places a *copy* or an *implementation* of this spec happens to live. The spec is the durable thing; everything that reads it is downstream and replaceable.

**This is the harness for everything else — including coding-agent harnesses.** A coding-agent harness (Hermes, Claude Code, an IDE assistant, a CI bot) is not a peer to this spec; it sits *inside* it. The spec is the outermost layer that wraps and governs every harness, tool, and workflow beneath it. So when a harness defines its own rules, those rules are expected to implement this spec — this spec does not implement them. If you think of your tools as harnesses that hold your work, this is the harness that holds the harnesses.

A compact, durable set of principles and standards for how work gets done — spanning engineering, security, communication, and operations. Each is **derived from a well-established framework** (named in *Foundations*), not invented; the value is the synthesis into one coherent, opinionated set with a clear rule for *when* each applies.

> **Scope of conformance:** this spec governs *every* tool, device, service, app, agent, or employment position Phil relies on. A system that contradicts it is misaligned and should be reconfigured, replaced, or — for a role — questioned. Conformance is the default expectation, not a nice-to-have.

> **Status of the rules:** these are *prevailing defaults for all substantial work*, not opt-in per task. "Substantial" = anything beyond a trivial one-off: work that produces a durable artifact, changes a system, affects a stakeholder, introduces or modifies a contract/source-of-truth/safety boundary, or will be repeated. A trivial one-off still obeys the one rule that costs nothing — *don't claim a side-effect succeeded without evidence*.

---

## What it means to conform

A tool, device, service, app, agent, or role **conforms to this spec (version 1.x)** when:

- It **upholds the standards by default**, not only when asked — substantial work follows them without per-task opt-in.
- Where it can't enforce a standard mechanically, it **doesn't silently violate it** — it surfaces the gap (fails loud) rather than quietly skipping.
- It treats this document (not its own local config) as the **authority** when the two conflict, except where a project's own contributing guidelines deliberately override an *operational* standard — in which case the override is explicit and stated.
- It can be pointed at the current spec version and **declare which version it implements**, so drift between the spec and an implementation is visible.

**Implementations are projections of the spec, not the source.** Hermes skills, a workstation's dotfiles, a project's `AGENTS.md`, a service's settings — each is a *binding* of this spec into a particular substrate. They implement it; they do not own it. When the spec changes, implementations are updated to match — never the reverse.

Conformance is graded, not binary: a system may fully implement some standards, partially others, and be unable to express a few. The goal is to **maximize conformance and make the gaps visible**, not to demand perfection from every substrate.

---

## How the principles are organized

- **Top-level principle** — frames how everything else is applied.
- **Core standards** — how substantial work is contracted, tracked, and proven.
- **Operational standards** — how work is executed and handled day-to-day.
- **Design principles** — how things are built and kept maintainable.
- **Communication standards** — how deliverables reach and read for their audience.
- **Domain principles** — first-principles sets for a specific field (e.g. security), applied on top of the general ones when working in that domain.

A standard fails *loud* (stop and surface it) rather than silently skipping. When in doubt, apply it.

---


## Top-level principle

### 0. System optimization — improve the whole, not one piece

Always optimize the **whole system**, not a local part. A change that improves the component in front of you while degrading the system overall is a regression. Check second-order effects; prefer shared leverage (a fix to a common layer) over one-off patches; work the binding constraint, not the convenient piece; improve coherence and discoverability, not just function.

This is the *objective function* the other standards serve. Simplify and automate **where it most improves the whole**.

*Foundation: Systems Thinking (Deming, Meadows); Theory of Constraints (Goldratt).*

---

## Core standards

### 1. Specifications — contract before build, when it's warranted

For substantial, hard-to-reverse, or contract-defining work, write the spec/design before building: success criteria, side-effect policy, source-of-truth boundary. Make the specification an executable contract, not decoration.

**Decision rule — spec vs. lightweight prose.** Require a spec/schema when the change introduces or modifies any of: external writes or publication gates; a source-of-truth hierarchy; an automation safety contract; a run manifest or coverage ledger; an output-hygiene validator; cross-surface consistency checks; background/scheduled execution policy. Lightweight prose is enough for minor wording fixes, a single guardrail patch, or local-only cleanup. On the boundary, prefer the spec — it fails loud and leaves a design record.

*Foundation: Spec-Driven Development; RFC/design-doc culture; Cynefin (match rigor to the problem's domain).*

### 2. Issue management — one visible source of truth for work

Track durable work in a single canonical, dependency-aware system. Capture meaningful work as a tracked item and close it with evidence rather than leaving it only in conversation. Don't run duplicate or competing trackers. Use dependencies and parent/child structure over loose notes. Reference external systems only by real, dereferenceable identifiers — never stuff internal taxonomy into an external-reference field.

*Foundation: Lean (make work visible; pull); DRY (one tracker, not many).*

### 3. Verification & Validation — prove it's right *and* right-for-purpose

Two distinct checks, both required:

- **Verification** ("did we build it right?") — conformance to required shape, schema, location, counts, hygiene. Mostly **mechanical**: a command or check with a deterministic pass/fail.
- **Validation** ("did we build the right thing?") — faithful to source evidence and intent. Mostly **judgment**: reasoning about meaning, audience, fidelity.

**The core rule:** *never report a step as done, synced, published, or correct unless a tool call or command actually returned evidence for it.* Reasoning that an action "should have" succeeded is not evidence.

**Mechanical vs. judgment.** If a command can prove it, it **must be run, not asserted**. Push as much verification as possible into the mechanical column — that's what survives being handed to a different person, agent, or model. For judgment work, expose the reasoning (a reconciliation table, a per-item rationale, a source citation) so it's auditable rather than asserted.

**Adversarial critique before presenting.** Before a near-final artifact reaches its audience, run a structured critique against a rubric (truth/support, audience fit, lede, completeness, confidence calibration, precision, hygiene, internal consistency). Prefer an **independent reviewer** over self-review — a fresh reviewer can't anchor on the author's choices. Findings must be **severity-classified and evidence-bound** (cite the specific line and reason); "no material issues" is a valid verdict when earned. A critique that rubber-stamps, or that manufactures nitpicks to look diligent, is worse than none.

**Gate taxonomy:** input · source · conformance · hygiene · build/test · fidelity · review · critique · fetch-back · closeout. Classify each gate as mechanical or judgment.

*Foundation: IEEE 1012 V&V; Lean Jidoka (build quality in / stop-the-line).*

---

## Operational standards

> A project's own contributing guidelines may override an operational standard; when they do, the project wins — and you state which rule you followed.

### 4. Commit conventions — atomic, conventional commits

One logical change per commit, using Conventional Commits format: `<type>(<scope>): <description>` (imperative, lowercase, no trailing period). Types: `feat`, `fix`, `docs`, `chore`, `refactor`, `style`, `test`, `ci`, `perf`. Each commit leaves the repo valid. Don't mix concerns; don't let a closeout/sync commit become a catch-all ("update various files" is an anti-pattern — split by purpose).

*Foundation: Conventional Commits spec; long-standing atomic-commit practice.*

### 5. Secret hygiene — no plaintext secrets, ever

Secrets never live in plaintext where they can leak, and are never printed.

- No tokens/keys/passwords/connection-strings in source, committed config, logs, notes, or URLs (`https://TOKEN@host` is forbidden).
- Keep credentials in a secret manager or OS keystore; inject **command-scoped**, not into the broad environment.
- Credential wrappers **fail closed** — refuse to run when the unlock gate is unavailable, never fall back to an unauthenticated path.
- Never print secret values; show `[REDACTED]`. Redact userinfo from URLs before displaying.
- When auth fails, verify the credential's *value shape* (prefix/length/provenance), not just its presence — but never log the value.

*Foundation: 12-Factor App (config in the environment); OWASP secret management.*

### 6. File layout — predictable, discoverable locations (XDG)

When a file location is a free choice, follow the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/latest/): config in `XDG_CONFIG_HOME`, durable data in `XDG_DATA_HOME`, state (logs/history/markers) in `XDG_STATE_HOME`, disposable cache in `XDG_CACHE_HOME`. Resolve these from the environment (with spec defaults), not hardcoded. Don't scatter new dotfiles in `$HOME` when an XDG location exists. Predictable placement is what makes things findable by people and tools alike.

*Foundation: XDG Base Directory Specification; convention over configuration.*

### 7. Session closeout — work isn't done until it's shipped AND shared

At the end of a unit of work: capture remaining work as tracked items, run quality gates if code changed, refresh any docs the change made stale, update status, and **integrate/push to the remote**. Verify the end state (local matches remote). Then **share it with whoever would benefit** — a teammate, a manager, a community, the person who asked. If a deliverable is meant for a particular person, team, org, or community, tell them before it is really done. Work is **not complete until the push succeeds and the right people know**.

This last part is a **habit worth building deliberately**, because the natural tendency is to under-share. So keep the friction low: **informal is the default** — a quick message, a status update, a one-line "shipped X, here's the link" usually suffices. Reserve formal write-ups for when the occasion genuinely calls for it. Don't let "I'd have to write something up" be the reason good work goes unshared. If a gate blocks the push, **preserve the work and report the exact unlock/retry path** — stranded-but-reported beats lost-and-silent. Never stop before pushing, and never say "ready to push when you are" — finish it.

*Foundation: CI/CD "done means shipped"; "you build it, you run it"; DORA lead-time; communication closes the loop shipping opens.*

### 8. Output hygiene — no internal identifiers across a trust boundary

Nothing shared with stakeholders or external audiences may leak internal/local identifiers, absolute machine paths, private tracker IDs, or credential material. Use audience-accessible sources or omit the metadata. Keep internal routing context in private records, never in shared artifacts.

*Foundation: least disclosure / need-to-know; data classification.*

### 9. Documentation — required, and refreshed with the code

Documentation is a **requirement for any development effort**, not an optional extra. A change with user-facing behavior, an interface, a setup/operation step, or a non-obvious decision is not complete until the documentation that explains it exists. And a **documentation refresh is part of maintenance**: when code changes, its docs are reviewed in the same pass and updated if stale — a change that leaves its docs describing old behavior is a defect, not a separate follow-up. Right-size the doc to the effort (design record, README, runbook, changelog, or agent-context file), keep one source of truth, and write it for its reader.

*Foundation: Agile (working software needs usable docs); Pragmatic Programmer (keep docs near the code, treat as part of the build).*

---

## Design principles

### 10. Reuse & simplicity — prefer existing tools; simple and elegant wins

Reuse wherever possible: before building, check whether an existing tool, library, or pattern already does it. Compose existing pieces before writing new ones. Choose the **smallest solution that fully solves the problem**. Prefer a well-understood existing tool over a marginally-better-fit bespoke one — the maintenance and cognitive cost of one-more-custom-thing usually outweighs the fit gain. Don't over-engineer for an imagined future (YAGNI); add abstraction when duplication proves it's needed, not preemptively. New bespoke code should justify why nothing existing fit.

*Foundation: Unix philosophy (do one thing well, compose small tools); KISS, DRY, YAGNI; "boring technology."*

### 11. Streamlined maintenance — automate the chore; humans avoid upkeep

Maintenance must be streamlined, because people don't reliably do recurring manual work — so it decays. Automate recurring chores with simple scripts/scheduled jobs. Prefer the **watchdog pattern**: silent when healthy, loud and actionable only when something needs attention, and fails loud (never silently) so a broken watchdog can't hide. Minimize touch points (zero-touch > one-touch). Keep the automation itself simple enough to read and fix quickly. (Cost/efficiency awareness and observability live here too: run the cheapest sufficient resource, and make state observable so you can manage it.)

*Foundation: Google SRE (eliminate toil; automate it); Lean (just-in-time, kaizen); Pragmatic Programmer (automate everything repeatable).*

### 12. Reliability & resilience — fail safe, degrade gracefully, recover fast

Assume things will fail; design so failure is **safe, visible, and recoverable**. Fail *closed* (not open) when a precondition is missing. Make operations **idempotent** by default — re-running must be safe, which is mandatory for anything retried or unattended. Preserve-and-report blocked work; never silently drop it. Retry once on transient/indexing latency before concluding failure. Degrade gracefully when a non-essential dependency is missing. Design for **fast recovery**: keep backups before destructive operations, prefer reversible changes, make the rollback path explicit.

*Foundation: AWS Well-Architected (reliability pillar); DORA (time-to-restore).*

### 13. Fast feedback / small reversible changes — small, safe, frequent beats big, infrequent

Prefer small, safe, reversible changes with fast feedback over large, infrequent, hard-to-reverse ones. Slice work thin — each slice leaves the system valid/shippable. Verify each slice quickly rather than batching all verification to the end. Integrate/push frequently; don't hoard completed work. Keep changes reversible (atomic commits, flags, backups). Prefer incremental over big-bang unless partial application would be genuinely unsafe (an atomic migration, a security fix that must land whole) — and state the reason when you choose big-bang.

*Foundation: DORA / Accelerate (small batch, short lead time, low change-failure, fast restore); Agile Manifesto (deliver working increments frequently).*

---

## Communication standards

Every deliverable has a reader. These make sure it is aimed and voiced for that reader.

### 14. Audience-tailoring — audience is a mandatory input; brevity wins

The **audience is a mandatory input to every deliverable**. Before writing, identify who will read or use it — their role, altitude, prior context, the decision or action it enables, and the trust boundary — and **tailor the output to them**. The same facts take a different shape per audience: executives want outcomes and decisions; an implementing engineer wants mechanics. Lead with what that audience needs. **Brevity wins:** say it in the fewest words that fully serve the audience; cut preamble, restatement, and filler. If two audiences need different things, write two tailored cuts, not one compromise that serves neither.

*Foundation: technical-communication practice (know your audience; bottom-line-up-front); Strunk & White ("omit needless words").*

### 15. Writing-style — match the author's voice, getting more precise over time

Prose written on someone's behalf must read like **they** wrote it, and the match must **improve over time**. Treat voice as a supervised, audience-specific profile: calibrate from real samples of their writing in that register, strip generic-AI tells, apply per draft, and fold reviewed edits back so each cycle is closer — an improvement ratchet, not a one-shot. Brevity applies here too. Anything external or published stays behind a review gate before it goes out.

*Foundation: persuasive/technical-writing craft; Strunk & White; deliberate practice (improve through reviewed feedback cycles).*

---

## Domain principles: security

The standards above are domain-general. Some fields have their own first-principles framework worth applying directly. For **security**, the touchstone is Rick Howard's *Cybersecurity First Principles* (Wiley, 2023): strip security back to one irreducible goal and derive everything from it, rather than chasing a disconnected best-practice checklist.

### S0. The absolute principle — reduce the probability of material impact

> **Reduce the probability of a material impact to the organization due to a cyber event, over time.**

Two words carry the weight. *Probability:* security is probabilistic, not binary — you lower likelihood, never reach zero. *Material:* only impact big enough to matter counts, which forces prioritization by consequence rather than by raw vulnerability count. A control is justified to the extent it measurably lowers the probability of *material* impact; if it doesn't ladder up to that, question it.

### S1–S5. The five derived strategies

1. **Zero Trust** — never trust by default; least-privilege, per-resource, continuously-verified access. Shrink the attack surface and blast radius so a compromise can't move freely. (Least-privilege, command-scoped, fail-closed credentials are Zero Trust applied to secrets — see standard #5.)
2. **Intrusion Kill Chain Prevention** — model the adversary's sequence of steps and break it at multiple stages. Defend against the *campaign*, not a single indicator; map controls to real adversary playbooks, not a generic checklist.
3. **Resilience** — assume prevention will sometimes fail; design so the organization survives and keeps delivering through an event. This is security's expression of the Reliability & resilience design principle (#12) — fail safe, degrade gracefully, recover fast.
4. **Risk Forecasting** — estimate the probability of material impact *quantitatively* and update it as evidence arrives (Bayesian reasoning, not red/yellow/green heat maps). You can't manage "reduce probability" if you can't estimate it; forecasts guide where the marginal security dollar goes.
5. **Automation** — **cuts across all four.** Encode the other strategies as code/infrastructure so they apply consistently, at scale, without manual toil or drift. This is security's expression of Streamlined maintenance (#11) and Fast feedback (#13).

*Foundation: Rick Howard, Cybersecurity First Principles (Wiley, 2023) — itself built on Zero Trust (Kindervag), the intrusion kill chain, resilience engineering, and Bayesian risk reasoning.*

---

## Foundations — the frameworks these derive from

These principles are deliberately built on durable, widely-validated bodies of thought rather than private theory. The point of naming them: when extending or questioning a principle, go back to the framework rather than re-deriving from scratch.

| Domain | Framework | Used for |
|---|---|---|
| Whole-system thinking | **Systems Thinking** (Deming, Meadows), **Theory of Constraints** (Goldratt) | System optimization; work the binding constraint |
| Matching approach to problem | **Cynefin** (Snowden) — clear / complicated / complex / chaotic / confusion | Spec-vs-prose rule; how much rigor/judgment a step needs |
| Flow, waste, improvement | **Lean / Toyota Production System** (Jidoka, Just-in-Time, kaizen) | Visible work; build quality in; automate toil; anti-overproduction |
| Delivery performance | **DORA / Accelerate** (deploy frequency, lead time, change-fail rate, time-to-restore) | Fast feedback; reliability/recovery; closeout |
| Architecture quality | **AWS Well-Architected** (operational excellence, security, reliability, performance, cost, sustainability) | Reliability; security; cost/efficiency; sustainability |
| Software-as-a-service config | **12-Factor App** | Secrets/config in the environment; disposability |
| Craft & code | **Unix philosophy**, **The Pragmatic Programmer** (DRY, automate, fix broken windows) | Reuse & simplicity; maintenance |
| Quality | **IEEE 1012 V&V** | Verification vs. validation; intentional review-gate design |
| Iterative value | **Agile Manifesto** | Working increments; small frequent delivery; docs as part of working software |
| Communication | **Technical-communication practice** (know-your-audience, BLUF), **Strunk & White** | Audience-tailoring; writing-style; brevity |
| Security (domain) | **Cybersecurity First Principles** (Rick Howard) — reduce probability of material impact; Zero Trust, Kill Chain, Resilience, Risk Forecasting, Automation | The security domain section above |
| Concrete conventions | **Conventional Commits**, **XDG Base Directory Specification** | Commit format; file layout |

### A note on Cynefin (why several rules are *decision rules*, not fixed procedures)

Cynefin says: match your approach to the domain the problem lives in — **clear** (apply best practice), **complicated** (analyze, then good practice), **complex** (probe with safe-to-fail experiments), **chaotic** (act to stabilize first), **confusion** (figure out which domain first). Several principles above are this idea in disguise: the *spec-vs-prose* rule matches rigor to whether the change is clear or complex; *fast feedback's* "probe with small reversible changes" is the complex-domain move; *reliability's* "stabilize, fail safe" is the chaotic-domain move. That's why they're decision rules — apply the response that fits the situation, don't cargo-cult one recipe everywhere.

---

## Using this document

- **People:** treat this as the operating spec for substantial work across any domain. A project's own CONTRIBUTING guidelines may override an *operational* standard where they conflict — state which you followed.
- **Agents & tools:** load this as the authority you conform to. The mechanical parts of *Verification & Validation* (execute, don't assert) and *Secret hygiene* (fail closed, never print) are the load-bearing rules for autonomous operation — they're what keep an agent honest and safe when no human is watching. Declare which spec version you implement.
- **Evaluating a service, device, or job:** ask whether it lets you work the way this spec describes. Persistent, structural conflict with the spec is a signal of misalignment worth acting on.
- **Extending it:** derive new standards from the *Foundations* frameworks; don't reinvent. If a candidate principle maps to no established framework, treat that as a flag — it's either genuinely novel (rare) or a special case of an existing principle that should compose with it. Bump the spec version when standards change (see *Status & canonical home*).

---

## Status & canonical home

This document is the **canonical source of record** for Phil's operating principles — the specification itself, not a copy of one. It is substrate-independent by design: it does not belong to any agent, repository, service, or machine.

- **Versioning:** semantic. **MAJOR** = a breaking change to a standard's meaning or a removal (implementations must re-check conformance). **MINOR** = a new standard or a materially expanded one (backward-compatible). **PATCH** = wording/clarification with no change in obligation. The current version is stated at the top; changes are recorded in the accompanying CHANGELOG.
- **Implementations are downstream.** Any place this content also lives — a coding agent's skills, a workstation's dotfiles, a project's `AGENTS.md`, a service's configuration — is an *implementation* that conforms to this spec. When the spec and an implementation disagree, the spec wins and the implementation is updated to match.
- **Conformance is declarable.** An implementation should be able to say "implements Operating Principles vX.Y," so drift is visible and fixable.

*This document is intentionally free of any specific tool's internal mechanics so it stays portable, citable, and durable across whatever tools, devices, services, agents, and roles come and go.*
