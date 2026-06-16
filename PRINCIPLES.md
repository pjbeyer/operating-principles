# Phil's Operating Principles — a personal specification

**Spec version: 0.3.0** · Status: pre-1.0 active draft · Canonical source of record (see *Status & canonical home* below)

This document is a **specification for how Phil's entire system of work should operate.** It is not documentation *about* a tool — it is the source specification that tools, devices, services, apps, agents, and even employment positions are expected to **conform to**. When Phil configures an AI agent, sets up a workstation, adopts a service, or evaluates a job, the question is: *does it operate the way this spec describes?*

It is deliberately **substrate-independent**. It is not tied to any coding agent, project repository, online service, or workstation. Those are all just places a *copy* or an *implementation* of this spec happens to live. The spec is the durable thing; everything that reads it is downstream and replaceable.

**This is the harness for everything else — including coding-agent harnesses.** A coding-agent harness (Hermes, Claude Code, an IDE assistant, a CI bot) is not a peer to this spec; it sits *inside* it. The spec is the outermost layer that wraps and governs every harness, tool, and workflow beneath it. So when a harness defines its own rules, those rules are expected to implement this spec — this spec does not implement them. If you think of your tools as harnesses that hold your work, this is the harness that holds the harnesses.

A compact, durable **pre-1.0** set of principles and standards for how work gets done — spanning engineering, security, communication, and operations. Each is **derived from a well-established framework** (named in *Foundations*), not invented; the value is the synthesis into one coherent, opinionated set with a clear rule for *when* each applies.

> **Scope of conformance:** this spec governs *every* tool, device, service, app, agent, or employment position Phil relies on. A system that contradicts it is misaligned and should be reconfigured, replaced, or — for a role — questioned. Conformance is the default expectation, not a nice-to-have.

> **Status of the rules:** these are *prevailing defaults for all substantial work*, not opt-in per task. "Substantial" = anything beyond a trivial one-off: work that produces a durable artifact, changes a system, affects a stakeholder, introduces or modifies a contract/source-of-truth/safety boundary, or will be repeated. A trivial one-off still obeys the one rule that costs nothing — *don't claim a side-effect succeeded without evidence*.

---

## What it means to conform

A tool, device, service, app, agent, or role **conforms to this pre-1.0 spec** when:

- It **upholds the standards by default**, not only when asked — substantial work follows them without per-task opt-in.
- Where it can't enforce a standard mechanically, it **doesn't silently violate it** — it surfaces the gap (fails loud) rather than quietly skipping.
- It treats this document (not its own local config) as the **authority** when the two conflict, except where a project's own contributing guidelines deliberately override an *operational* standard — in which case the override is explicit and stated.
- It can be pointed at the current spec version and **declare which version it implements**, so drift between the spec and an implementation is visible.

**Implementations are projections of the spec, not the source.** Hermes skills, a workstation's dotfiles, a project's `AGENTS.md`, a service's settings — each is a *binding* of this spec into a particular substrate. They implement it; they do not own it. When the spec changes, implementations are updated to match — never the reverse.

Conformance is graded, not binary: a system may fully implement some standards, partially others, and be unable to express a few. The goal is to **maximize conformance and make the gaps visible**, not to demand perfection from every substrate.

**Hard vs. soft rules.** Each standard's individual rules are either *hard* or *soft*:

- **Hard rules** must never be violated, no matter the convenience — e.g. *never claim a side-effect succeeded without evidence*, *never write a plaintext secret or print one*, *credential wrappers fail closed*, *no internal identifiers across a trust boundary*. A system that breaks a hard rule is non-conformant, full stop.
- **Soft rules** are strong defaults that may yield to a stated, justified reason — e.g. *prefer small reversible changes*, *match voice from a sample*, *spec before build*. Yielding is allowed when you say why; silently ignoring is not.

When an implementation can mark its rules, it should label each hard or soft (as in a machine-readable preference file), so the non-negotiable core is unambiguous. Hard rules are the load-bearing safety/honesty floor; soft rules are the craft.

**Principles as decision algorithms.** A principle should be usable before the decision is made, not only as a slogan afterward. It states how to choose when the situation recurs, exposes the tradeoff it governs, and can be debated, revised, and versioned as evidence accumulates. Good principles turn repeated judgment into a reusable decision system while preserving room for context and integrity. Painful misses are especially valuable inputs: pain plus reflection becomes progress when the lesson is captured, attributed, and folded back into the system rather than merely endured.[^dalio-principles][^dalio-pain]

---

## How the principles are organized

- **Top-level principles** — define the objective function and non-negotiable floor.
- **Core standards** — how substantial work is contracted, tracked, and proven.
- **Operational standards** — how work is executed and handled day-to-day.
- **Design principles** — how things are built and kept maintainable.
- **Communication standards** — how deliverables reach and read for their audience.
- **Domain principles** — first-principles sets for a specific field (e.g. security), applied on top of the general ones when working in that domain.

A standard fails *loud* (stop and surface it) rather than silently skipping. When in doubt, apply it.

---


## Top-level principles

### 0a. System optimization — improve the whole, not one piece

Always optimize the **whole system**, not a local part. A change that improves the component in front of you while degrading the system overall is a regression. Check second-order effects — including lagged consequences, feedback delays, oscillation, and overshoot. Prefer shared leverage (a fix to a common layer) over one-off patches; work the binding constraint, not the convenient piece; improve coherence and discoverability, not just function.

Use **ranked intervention** when changing a system: goals, structures, rules, and feedback loops usually matter more than parameter tweaks. Remember **requisite variety**: a controller must have enough range to absorb the variety of the system it regulates, so complex systems need responses with enough flexibility, observability, and escalation paths. And use **purpose from behavior** as a truth test: a system's real purpose is what it actually does, not what its documentation says it intends.

Treat the **system that produces the work** as part of the work. The environment, specification, checks, templates, review agents, captured learnings, and release process that produce an output often matter more than any single output. Spend meaningful effort improving that machine; every cycle should leave the system better for the next.

This is the *objective function* the other standards serve. Simplify and automate **where it most improves the whole**.

*Foundation: Systems Thinking (Deming, Meadows); Theory of Constraints (Goldratt); cybernetics (Ashby); compound engineering / harness engineering.*[^meadows][^ashby]

### 0b. Integrity — the non-negotiable floor

Optimize the system only inside an **integrity floor**. System optimization is the objective function; integrity is the constraint. It is not another preference to trade off against speed, elegance, or output volume. A locally efficient action that violates the floor is not a better optimization — it is outside the allowed solution space.

The floor is:

- **Honesty by default** — don't fabricate, exaggerate, hide uncertainty, or imply evidence you do not have.
- **Non-maleficence** — avoid foreseeable harm; fail closed where harm or trust-boundary violations are plausible.
- **Transparency about uncertainty and limits** — say what is known, what is inferred, what is unverified, and what could change the conclusion.
- **Accountability** — make consequential actions attributable, reviewable, and correctable; own mistakes and feed them back into the system.

Many hard rules in this spec are integrity operating in specific domains: execute-don't-assert, no plaintext secrets, output hygiene, and always-gated decisions around money/security/destructive ops/communications in Phil's name.

*Foundation: Beauchamp & Childress; Belmont Report; ACM/IEEE professional ethics codes; common-morality honesty norms.*[^beauchamp-childress][^belmont][^acm-code][^ieee-code]

---

## Core standards

### 1. Specifications — contract before build, when it's warranted

For substantial, hard-to-reverse, or contract-defining work, write the spec/design before building: success criteria, side-effect policy, source-of-truth boundary. Make the specification an executable contract, not decoration.

**Decision rule — spec vs. lightweight prose.** Require a spec/schema when the change introduces or modifies any of: external writes or publication gates; a source-of-truth hierarchy; an automation safety contract; a run manifest or coverage ledger; an output-hygiene validator; cross-surface consistency checks; background/scheduled execution policy. Lightweight prose is enough for minor wording fixes, a single guardrail patch, or local-only cleanup. On the boundary, prefer the spec — it fails loud and leaves a design record.

*Foundation: Spec-Driven Development; RFC/design-doc culture; Cynefin (match rigor to the problem's domain).*

### 2. Issue management — one visible source of truth for work

Track durable work in a single canonical, dependency-aware system. Capture meaningful work as a tracked item and close it with evidence rather than leaving it only in conversation. Don't run duplicate or competing trackers. Use dependencies and parent/child structure over loose notes. Reference external systems only by real, dereferenceable identifiers — never stuff internal taxonomy into an external-reference field.

**Capture before clarity.** Capture every idea, task, or observation *immediately*, however vague — speed of capture beats quality of capture. Don't block a capture on categorization, prioritization, or full understanding; refine it later as context emerges. The cost of a messy capture is near zero; the cost of a lost insight is unrecoverable. The default action for any new thought is to create the tracked item with whatever title exists in the moment.

*Foundation: Lean (make work visible; pull); DRY (one tracker, not many); GTD (capture everything, clarify later).*

### 3. Verification & Validation — prove it's right *and* right-for-purpose

Two distinct checks, both required:

- **Verification** ("did we build it right?") — conformance to required shape, schema, location, counts, hygiene. Mostly **mechanical**: a command or check with a deterministic pass/fail.
- **Validation** ("did we build the right thing?") — faithful to source evidence and intent. Mostly **judgment**: reasoning about meaning, audience, fidelity.

**The core rule:** *never report a step as done, synced, published, or correct unless a tool call or command actually returned evidence for it.* Reasoning that an action "should have" succeeded is not evidence.

**Mechanical vs. judgment.** If a command can prove it, it **must be run, not asserted**. Push as much verification as possible into the mechanical column — that's what survives being handed to a different person, agent, or model. For judgment work, expose the reasoning (a reconciliation table, a per-item rationale, a source citation) so it's auditable rather than asserted.

**Adversarial critique before presenting.** Before a near-final artifact reaches its audience, run a structured critique against a rubric (truth/support, audience fit, lede, completeness, confidence calibration, precision, hygiene, internal consistency). Prefer an **independent reviewer** over self-review — a fresh reviewer can't anchor on the author's choices. Findings must be **severity-classified and evidence-bound** (cite the specific line and reason); "no material issues" is a valid verdict when earned. A critique that rubber-stamps, or that manufactures nitpicks to look diligent, is worse than none.

**Gate taxonomy:** input · source · conformance · hygiene · build/test · fidelity · review · critique · fetch-back · closeout. Classify each gate as mechanical or judgment.

**Human review gates are designed intentionally** — not reflexive, not permanent. Classify each side-effecting gate as **graduating** (start gated; step down toward automation as it earns *evidence of clean, reversible, side-effect-safe runs*) or **always-gated** (keeps a human gate no matter how good it gets — irreversible publication, money/credentials/security posture, destructive ops without clean undo, communications in your name). State the class and why; never silently drop a gate because output "looked good lately."

**Trust graduates on evidence (the autonomy ratchet).** An automated actor *earns* autonomy by demonstrating accuracy over real runs, and can lose it: review-every-run → spot-check → dry-run-only → fully automated, stepping back a level on a failure. Wrong outputs are corrected inline; *systematic* mistakes are filed as defects and fed back so the actor improves. The human's role shifts from executor to architect/overseer — designing the pipelines, reviewing the high-trust gates, and promoting or demoting trust tiers. This is how a small team (or one person) scales through automation without surrendering the always-gated decisions.

*Foundation: IEEE 1012 V&V; Lean Jidoka (build quality in / stop-the-line); progressive-autonomy / trust-tier practice.*

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

Documentation is a **requirement for any development effort**, not an optional extra. A change with user-facing behavior, an interface, a setup/operation step, or a non-obvious decision is not complete until the documentation that explains it exists. And a **documentation refresh is part of maintenance**: when code changes, its docs are reviewed in the same pass and updated if stale — a change that leaves its docs describing old behavior is a defect, not a separate follow-up.

Use **write-to-think** for important work: externalizing reasoning into a spec, decision record, memo, or commit message is part of the thinking, not merely a report after thinking is done. Writing exposes gaps, contradictions, and missing evidence. Right-size the doc to the effort (design record, README, runbook, changelog, or agent-context file), keep one source of truth, and write it for its reader.

*Foundation: Agile (working software needs usable docs); Pragmatic Programmer (keep docs near the code, treat as part of the build); knowledge-work note-making practice.*

### 10. Version-aware state — persisted state carries version metadata

Any durable, persisted state (config files, data files, schemas, specs, this document) carries a **version** so schema evolution and migration are safe. Use semantic versioning; timestamps in ISO 8601. Machine state uses structured metadata (e.g. a `_version` field); human-editable files (preference docs, agent-context files) may use a friendlier `version` in frontmatter and skip mandatory timestamps. Without version metadata, migrations become guesswork and silent corruption creeps in.

*Foundation: schema-evolution / migration practice; semantic versioning.*

### 11. Time-boxed exploration — bound the open-ended, force a decision

Experiments, investigations, and exploratory work get an explicit **time box set before starting** (recorded in the tracked item or notes). At the limit, choose one of three outcomes: **continue** (with a new, justified box), **park** (archive with state + re-entry conditions), or **discard** (close it, delete throwaway artifacts). Viable work graduates to a real project; dead work gets closed, not left open indefinitely. Unbounded exploration becomes a graveyard — time boxes force the decision points that keep the backlog honest and the workspace light.

*Foundation: Lean (timeboxing, limit WIP); Agile spikes; Cynefin (safe-to-fail probes in the complex domain).*

### 12. Probabilistic judgment & calibration — beliefs should carry odds

For uncertain judgments, reason in probabilities and expected value instead of binary confidence. Anchor on base rates and reference classes before privileging the vivid case in front of you. State confidence in a way that can later be checked against reality, and judge decisions by the quality of the process given what was known at the time — not only by the outcome. When the stakes justify it, use premortems, prediction logs, and calibration review so belief quality improves over time.

This is Verification & Validation applied to beliefs: don't merely assert confidence; make it auditable.

*Foundation: decision theory; Tversky & Kahneman on heuristics and biases; Tetlock on forecasting; Annie Duke on resulting and decision quality.*[^tversky-kahneman][^kahneman][^tetlock][^duke]

### 13. Execution right-sizing — match mechanism, model, and effort to task structure

Use the smallest sufficient execution style:

- **Routine / well-understood work** → deterministic workflows: checklists, templates, scripts, prompt chains, and explicit gates.
- **Open-ended / brittle-to-script work** → agentic or exploratory automation, with bounded autonomy and review gates.
- **Simple / low-stakes work** → cheap, fast, low-effort resources.
- **Complex / high-stakes work** → stronger models, higher effort, independent critique, and stricter validation.

Do not use an expensive or open-ended agent when a checklist would be clearer; do not force a rigid checklist onto a genuinely complex task that needs sensing, adaptation, or judgment. Direction should be **outcome-first**: specify the desired result, example, format, destination, boundaries, and review gate; let the executor choose the implementation path inside those constraints.

*Foundation: Anthropic's workflow-vs-agent distinction; Cynefin; delegation practice; cost/quality allocation.*[^anthropic-agents]

---

## Design principles

### 14. Reuse & simplicity — prefer existing tools; simple and elegant wins

Reuse wherever possible: before building, check whether an existing tool, library, or pattern already does it. Compose existing pieces before writing new ones. Choose the **smallest solution that fully solves the problem**. Prefer a well-understood existing tool over a marginally-better-fit bespoke one — the maintenance and cognitive cost of one-more-custom-thing usually outweighs the fit gain. Don't over-engineer for an imagined future (YAGNI); add abstraction when duplication proves it's needed, not preemptively. New bespoke code should justify why nothing existing fit.

*Foundation: Unix philosophy (do one thing well, compose small tools); KISS, DRY, YAGNI; "boring technology."*

**Hierarchy-first / one home per fact.** Information lives at *exactly one level* and is referenced, never duplicated. When a narrower, more-specific rule genuinely conflicts with a broader default, the narrower applicable rule wins — but it should reference the broader rule rather than copy it. Put a fact at the broadest level it applies to (global → profile/area → project → component) and reference it from narrower levels rather than copying it down. Duplication is how drift starts: when the same thing lives in two places, one gets updated and the other silently lies. Before adding information, decide the right level; if it applies broadly, it belongs at the broad level, not pasted into each consumer.

*Foundation: DRY / single-source-of-truth; layered configuration (broad defaults, narrow overrides).*

### 15. Streamlined maintenance — automate the chore; humans avoid upkeep

Maintenance must be streamlined, because people don't reliably do recurring manual work — so it decays. Use a lightweight PDCA loop: log wins, misses, and surprises; convert repeated fixes into standards; periodically prune, merge, or retire rules that no longer pull their weight. Automate recurring chores with simple scripts/scheduled jobs. Prefer the **watchdog pattern**: silent when healthy, loud and actionable only when something needs attention, and fails loud (never silently) so a broken watchdog can't hide. Minimize touch points (zero-touch > one-touch). Keep the automation itself simple enough to read and fix quickly. (Cost/efficiency awareness and observability live here too: run the cheapest sufficient resource, and make state observable so you can manage it.)

*Foundation: Google SRE (eliminate toil; automate it); Lean (just-in-time, kaizen); Pragmatic Programmer (automate everything repeatable).*

### 16. Reliability & resilience — fail safe, degrade gracefully, recover fast

Assume things will fail; design so failure is **safe, visible, and recoverable**. Fail *closed* (not open) when a precondition is missing. Make operations **idempotent** by default — re-running must be safe, which is mandatory for anything retried or unattended. Preserve-and-report blocked work; never silently drop it. Retry once on transient/indexing latency before concluding failure. Degrade gracefully when a non-essential dependency is missing. Design for **fast recovery**: keep backups before destructive operations, prefer reversible changes, make the rollback path explicit.

*Foundation: AWS Well-Architected (reliability pillar); DORA (time-to-restore).*

### 17. Fast feedback / small reversible changes — small, safe, frequent beats big, infrequent

Prefer small, safe, reversible changes with fast feedback over large, infrequent, hard-to-reverse ones. Slice work thin — each slice leaves the system valid/shippable. Verify each slice quickly rather than batching all verification to the end. Integrate/push frequently; don't hoard completed work. Keep changes reversible (atomic commits, flags, backups). Prefer incremental over big-bang unless partial application would be genuinely unsafe (an atomic migration, a security fix that must land whole) — and state the reason when you choose big-bang.

*Foundation: DORA / Accelerate (small batch, short lead time, low change-failure, fast restore); Agile Manifesto (deliver working increments frequently).*

---

## Communication standards

Every deliverable has a reader. These make sure it is aimed and voiced for that reader.

### 18. Audience-tailoring — audience is a mandatory input; brevity wins

The **audience is a mandatory input to every deliverable**. Before writing, identify who will read or use it — their role, altitude, prior context, the decision or action it enables, and the trust boundary — and **tailor the output to them**. The same facts take a different shape per audience: executives want outcomes and decisions; an implementing engineer wants mechanics. Lead with what that audience needs. **Brevity wins:** say it in the fewest words that fully serve the audience; cut preamble, restatement, and filler. If two audiences need different things, write two tailored cuts, not one compromise that serves neither.

*Foundation: technical-communication practice (know your audience; bottom-line-up-front); Strunk & White ("omit needless words").*

**Graduated output quality — match polish to audience and purpose.** Not all output deserves the same polish; over-polishing internal work wastes time, under-polishing external work erodes trust. Match the standard to the tier:

| Tier | Audience | Standard |
|---|---|---|
| Internal / exploratory | Self, agents | MVP. Rough notes, incomplete thoughts, throwaway experiments. Must *not* be over-polished. |
| Team-facing | Your team / collaborators | Clear and accurate. Consistent format. Reviewed before sharing. |
| Stakeholder-facing | Execs, clients, board, public | Polished, precise, on-cadence. Data verified. No ambiguity in recommendations or risk statements. |

When unsure of the tier, default to team-facing. Matching effort to audience is a resource-allocation decision, not a quality compromise.

### 19. Writing-style — match the author's voice, getting more precise over time

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
3. **Resilience** — assume prevention will sometimes fail; design so the organization survives and keeps delivering through an event. This is security's expression of the Reliability & resilience design principle (#16) — fail safe, degrade gracefully, recover fast.
4. **Risk Forecasting** — estimate the probability of material impact *quantitatively* and update it as evidence arrives (Bayesian reasoning, not red/yellow/green heat maps). You can't manage "reduce probability" if you can't estimate it; forecasts guide where the marginal security dollar goes.
5. **Automation** — **cuts across all four.** Encode the other strategies as code/infrastructure so they apply consistently, at scale, without manual toil or drift. This is security's expression of Streamlined maintenance (#15) and Fast feedback (#17).

*Foundation: Rick Howard, Cybersecurity First Principles (Wiley, 2023) — itself built on Zero Trust (Kindervag), the intrusion kill chain, resilience engineering, and Bayesian risk reasoning.*

---

## Domain principles: knowledge & learning

When the work is learning, expertise-building, or knowledge-base design, apply these on top of the general standards.

- **Atomic, durable notes.** Capture ideas in small units that can be linked, revised, and reused; progressive summarization and evergreen notes are tools for making knowledge compound.
- **Retrieval beats rereading.** Spacing, interleaving, and retrieval practice are usually stronger learning mechanisms than passive review.
- **Practice deliberately.** Expertise improves through focused practice, immediate feedback, and work at the edge of ability.
- **Hierarchy and links are complements.** Keep one canonical home per fact, then link to it liberally; linking-over-foldering must not become duplication-over-truth.

*Foundation: Forte's CODE/progressive-summarization practice; Ahrens and Luhmann-inspired note-making; Bjork desirable difficulties; Ericsson deliberate practice; Roediger/McDaniel learning science.*[^forte][^ahrens][^bjork][^ericsson]

---

## Domain principles: AI agent operations

When building or operating AI agents/automations, apply these on top of the general standards.

- **Harness as product.** Treat agent context, specs, checks, prompts, templates, and review loops as the product surface that produces future work. Keep context files as short indexes, not manuals; move detail into structured, versioned references.
- **Context-loading discipline.** Prefer lazy/on-demand references over eager-loading everything. Use explicit links for context an agent must load; batch independent reads.
- **Trigger and recurrence design.** Automations should have high-signal triggers, bounded scopes, clear quiet/success behavior, and explicit escalation paths.
- **Mutation safety pre-flight.** View before editing; avoid destructive whole-content replaces; anchor targeted edits to stable surrounding text; ask when the target or trust boundary is unclear.

*Foundation: Anthropic workflows/agents guidance; OpenAI harness-engineering practice; spec-driven development; Phil's Notion AI Tools operating model.*[^anthropic-agents]

---

## Domain principles: human agency & ethics

Integrity is always-on; these situational practices apply when work acts on, represents, or materially affects people.

- **Informed consent.** Act on a person's behalf only with their understanding and agreement, especially when publishing, messaging, spending, changing access, or making commitments in their name.
- **Conflicts of interest.** Disclose and manage divided loyalties, incentives, or constraints that could distort judgment.
- **Transparency and accountability.** For consequential decisions, keep enough record that the decision can be reviewed, corrected, or appealed.

*Foundation: Belmont Report; Beauchamp & Childress; ACM/IEEE professional ethics codes.*[^belmont][^beauchamp-childress][^acm-code][^ieee-code]

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
| Iterative value | **Agile Manifesto** | Working increments; small frequent delivery; docs as part of working software; timeboxed spikes |
| Personal productivity | **GTD** (Getting Things Done — capture, clarify later) | Capture-before-clarity; one trusted system |
| Autonomy & oversight | **Progressive-autonomy / trust-tier practice**; **workflow-vs-agent guidance**; harness engineering | Trust graduates on evidence; human as architect/overseer; intentional gates; execution right-sizing |
| Judgment & behavior | **Tversky/Kahneman heuristics and biases**, **forecasting/calibration**, **behavioral economics / choice architecture** | Probabilistic judgment; debiasing backlog; calibration; decision hygiene |
| Personal operating systems | **Ray Dalio, Principles** | Explicit principles as decision algorithms; pain + reflection; believability-weighted input; mistake learning |
| State evolution | **Semantic versioning**, schema-migration practice | Version-aware state; this spec's own versioning |
| Communication | **Technical-communication practice** (know-your-audience, BLUF), **Strunk & White** | Audience-tailoring; graduated output quality; writing-style; brevity |
| Security (domain) | **Cybersecurity First Principles** (Rick Howard) — reduce probability of material impact; Zero Trust, Kill Chain, Resilience, Risk Forecasting, Automation | The security domain section above |
| Concrete conventions | **Conventional Commits**, **XDG Base Directory Specification** | Commit format; file layout |

### A note on Cynefin (why several rules are *decision rules*, not fixed procedures)

Cynefin says: match your approach to the domain the problem lives in — **clear** (apply best practice), **complicated** (analyze, then good practice), **complex** (probe with safe-to-fail experiments), **chaotic** (act to stabilize first), **confusion** (figure out which domain first). Several principles above are this idea in disguise: the *spec-vs-prose* rule matches rigor to whether the change is clear or complex; *fast feedback's* "probe with small reversible changes" is the complex-domain move; *reliability's* "stabilize, fail safe" is the chaotic-domain move. That's why they're decision rules — apply the response that fits the situation, don't cargo-cult one recipe everywhere.

---

## How this spec grows — the domain-examination method

New standards are not invented; they are **extracted from domains of expertise and grounded in that domain's established first principles.** This is the repeatable method for examining a domain and deciding what, if anything, becomes a standard. It exists so the spec expands deliberately and stays grounded, instead of accumulating ad-hoc opinions.

1. **Pick a domain** from the repo-local Beads backlog — a field with a mature body of thought (e.g. decision-making, knowledge management, learning, negotiation, systems theory).
2. **Find its established first principles.** Identify the canonical frameworks, thinkers, and primary sources the field already agrees on. Borrow; don't re-derive. If you can't find an established foundation, that's a signal the candidate is folklore, not a principle.
3. **Extract candidate principles** — the irreducible ideas, stated as the domain states them, with the source named.
4. **Classify each candidate:**
   - **General** — applies across most work regardless of field → promote to a core/operational/design/communication standard.
   - **Domain-specific** — only meaningful inside that field → a *domain principles* section (like security), applied on top of the general standards when working there.
   - **Already covered** — a restatement or special case of an existing standard → fold in as a sharpening, with a cross-reference, not a new entry.
   - **Folklore** — maps to no established framework and isn't broadly useful → discard, or hold until evidence accrues.
5. **Check the hierarchy fit** — place each kept principle at the right level (global standard, domain section, or a downstream implementation's local override). Don't globalize something that's really project- or role-specific (standard #14, hierarchy-first).
6. **Record lineage** — every kept standard names its *Foundation*. No foundation, no promotion.
7. **Version and propagate** — bump the spec version, update the CHANGELOG, then propagate to the downstream implementations.

The bar for promotion to a *general* standard is high: broad applicability **and** an established foundation **and** a clear when-to-apply rule. When in doubt, file it as a domain principle or a sharpening rather than inflating the core.

### Domain backlog

The domain backlog is tracked in this repository's Beads instance, not in committed markdown lists. Use `bd ready`, `bd list`, and parent/child Beads relationships to inspect active candidates. Keeping the backlog in Beads preserves dependencies, status, comments, and sync history without turning this spec into a task list. Examined domains move into standards or domain sections with lineage recorded here and complete citations in endnotes.

---

## Using this document

- **People:** treat this as the operating spec for substantial work across any domain. A project's own CONTRIBUTING guidelines may override an *operational* standard where they conflict — state which you followed.
- **Agents & tools:** load this as the authority you conform to. The mechanical parts of *Verification & Validation* (execute, don't assert) and *Secret hygiene* (fail closed, never print) are the load-bearing rules for autonomous operation — they're what keep an agent honest and safe when no human is watching. Declare which spec version you implement.
- **Evaluating a service, device, or job:** ask whether it lets you work the way this spec describes. Persistent, structural conflict with the spec is a signal of misalignment worth acting on.
- **Extending it:** derive new standards from the *Foundations* frameworks; don't reinvent. If a candidate principle maps to no established framework, treat that as a flag — it's either genuinely novel (rare) or a special case of an existing principle that should compose with it. Bump the spec version when standards change (see *Status & canonical home*).

---

## Status & canonical home

This document is the **canonical source of record** for Phil's operating principles — the specification itself, not a copy of one. It is substrate-independent by design: it does not belong to any agent, repository, service, or machine.

- **Versioning:** semantic, but **pre-1.0** until the first stable public release. While `0.x`, **MINOR** versions may still reshape obligations and implementations must re-check conformance; **PATCH** versions are clarifications/fixes. The project uses Release Please to manage release PRs, changelog entries, and tags.
- **Implementations are downstream.** Any place this content also lives — a coding agent's skills, a workstation's dotfiles, a project's `AGENTS.md`, a service's configuration — is an *implementation* that conforms to this spec. When the spec and an implementation disagree, the spec wins and the implementation is updated to match.
- **Conformance is declarable.** An implementation should be able to say "implements Operating Principles v0.x" (or later v1.x), so drift is visible and fixable.

---

## Endnotes

[^dalio-principles]: Ray Dalio, *Principles: Life and Work* (Simon & Schuster, 2017); official Principles site, https://www.principles.com/; Simon & Schuster publisher page, https://www.simonandschuster.com/books/Principles/Ray-Dalio/9781501124020.
[^dalio-pain]: Ray Dalio, "Pain + Reflection = Progress," official Principles entry, https://www.principles.com/principles/5f4aaa06-72de-413a-981d-62b0cc13ca21/.
[^tversky-kahneman]: Amos Tversky and Daniel Kahneman, "Judgment under Uncertainty: Heuristics and Biases," *Science* 185, no. 4157 (1974): 1124–1131, doi:10.1126/science.185.4157.1124, https://pubmed.ncbi.nlm.nih.gov/17835457/.
[^kahneman]: Daniel Kahneman, *Thinking, Fast and Slow* (Farrar, Straus and Giroux, 2011).
[^tetlock]: Philip E. Tetlock and Dan Gardner, *Superforecasting: The Art and Science of Prediction* (Crown, 2015).
[^duke]: Annie Duke, *Thinking in Bets: Making Smarter Decisions When You Don't Have All the Facts* (Portfolio, 2018).
[^meadows]: Donella H. Meadows, "Leverage Points: Places to Intervene in a System" (Sustainability Institute, 1999); Donella H. Meadows, *Thinking in Systems* (Chelsea Green, 2008).
[^ashby]: W. Ross Ashby, *An Introduction to Cybernetics* (Chapman & Hall, 1956).
[^anthropic-agents]: Anthropic, "Building Effective Agents" (2024), https://www.anthropic.com/research/building-effective-agents.

[^belmont]: National Commission for the Protection of Human Subjects of Biomedical and Behavioral Research, *The Belmont Report* (1979), https://www.hhs.gov/ohrp/regulations-and-policy/belmont-report/.
[^beauchamp-childress]: Tom L. Beauchamp and James F. Childress, *Principles of Biomedical Ethics*, 8th ed. (Oxford University Press, 2019).
[^acm-code]: Association for Computing Machinery, *ACM Code of Ethics and Professional Conduct* (2018), https://www.acm.org/code-of-ethics.
[^ieee-code]: IEEE, *IEEE Code of Ethics*, https://www.ieee.org/about/corporate/governance/p7-8.html.
[^forte]: Tiago Forte, *Building a Second Brain* (Atria Books, 2022).
[^ahrens]: Sönke Ahrens, *How to Take Smart Notes* (Sönke Ahrens, 2017).
[^bjork]: Robert A. Bjork and Elizabeth L. Bjork, "Making Things Hard on Yourself, But in a Good Way: Creating Desirable Difficulties to Enhance Learning," in *Psychology and the Real World*, 2nd ed. (Worth, 2014).
[^ericsson]: K. Anders Ericsson and Robert Pool, *Peak: Secrets from the New Science of Expertise* (Eamon Dolan/Houghton Mifflin Harcourt, 2016).

*This document is intentionally free of any specific tool's internal mechanics so it stays portable, citable, and durable across whatever tools, devices, services, agents, and roles come and go.*
