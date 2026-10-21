English | [简体中文](./CHANGELOG.md)

# CHANGELOG — autopilot

Single version scheme: `V2.00N`. (Early private iterations used internal vNN
numbers — v41=V2.001, v43=V2.002, v44=V2.003, v45=V2.004, v46=V2.005,
v47=V2.006, v48=V2.007, v49=V2.008. Retired as of V2.008.)

**V2.037** — Closeout order and scope: the central entry is appended and read back before the final message; “what is worth improving / review this repo” is a read-only survey; setup may ship as a same-round chore commit; a harness-refused skill is inline, not missing.

**V2.036** — Read-only is a task: read-only/query rounds still need T0 (ask-matt tool/inline), the card/refresh, and a central entry; lane=none is not an exemption.

**V2.035** — Order and isolation: code-review closes the chain (tdd/implement before it); a single-round subagent may put the card in NOTES and repeat it in the final message; delegation depth 0 counts as no-subagent harness; Lane B self-answered grill does not require calling grilling/domain-modeling; eval material is moved out of the repo during test windows.

**V2.034** — Log discipline: typo/doc/single config-row work is Lane A, never na; even na rounds write and commit; Audit must not point at LOGBOOK-RECEIPT; PASS-gaps(n) counts the 6-step gate list; an installed-but-refused skill is inline-read, never bundled-fallback; the card carries an invocation-surface line.

**V2.033** — Log consistency: read-only/query rounds no longer write a child receipt; `chain` must equal `Skills called` in order and cover every artifact skill; B–E need ≥2, Lane A/read-only may run one; the ledger gains a `self-check` line; the project-notes pointer must be an existing file; repo-state/central-log queries use the read-only protocol; setup only in the first round before implementation.

**V2.032** — Log instrumentation: a hermetic logbook via `.autopilot/usage-log-path` (evals never touch the production book), a multi-frame transcript decoder, a canary self-check (rubric ⑩; a broken judge invalidates the run), and two-rate log metrics; tightened `PASS-gaps(n)` and reflection quote requirements.

**V2.031** — Log evidence: the task entry becomes a receipt ledger (chain / artifact map / rule-level blockers with file:line / landed receipt / log ownership); friction tickets are written only when something went wrong; reflections become event-triggered observation cards (recovery / declared-vs-executed / conflicting rules / uncovered paths / decidability). Closeout must read the `landed` line back; child sessions write a receipt. The narrative five aspects and the “gap/other” questions are retired.

**V2.030** — Invocation capability: when a harness honors `disable-model-invocation` (DSH), a refused Skill-tool call does not mean the skill is missing — the driver reads the installed body inline, records `调用面:` + `name(inline)` + `file:line`, and never retries the refused call. T0 belongs to `ask-matt` (tool or inline); loading autopilot itself is not T0.

**V2.029** — Log boundary: the central logbook records **skill-side friction
only** (which skill should have fired, which rule was vague, which gate was
bypassed, what broke in the logging/reflection machinery); project-domain
material (root causes, decisions, thresholds, ops details, next-round state)
lives in the project's own `NOTES.md` / spec / `docs/`, with a single
`Project notes:` pointer left in the logbook. Every task entry carries a
`Log ownership: skill` line; reflection entries are headed skill-side and must
point back at a skill file.

**V2.028** — Packaging fix: the SKILL.md description is now a YAML-legal scalar
(an unquoted `: ` made strict parsers drop the whole skill — DSH did); a
frontmatter packaging gate was added.

**V2.027** — Opt-in per project: autopilot takes over only when an `AGENTS.md`
between the cwd and the repo root carries the standalone line `autopilot: on`
(`autopilot: off` vetoes); the global instruction becomes a default-off gate;
the skill description splits explicit asks (unconditional) from implicit task
shapes (credential required).

**V2.026** — Pre-trust: red-team the conclusion itself before adoption; gate-landing
checklist (satisfiability example, never-red argument, worst-case constants,
coverage statement); readings cite their writer; parallel write-boundary rules.

**V2.025** — Execution trust: every round emits a kickoff card (task/lane/tier/
skill-list/chain·product/first action) before any work — no card, not started;
per-round re-anchor plus conditional re-read replaces "later rounds skip the
re-read"; no product = that step did not happen (product/deviation/audit lines);
full|lite|na tier discipline; read-only/query minimal protocol; closing
read-only audit pass; trigger-layer templates (global/project hooks, /autopilot
command, see the repo's deploy/).

**V2.024** — Closeout trust: the central entry belongs to the working lane,
round settlement (b-round replacement / increment accounting / closeout evidence
checklist), reflection counting unit.

**V2.023** — Enforcement hardening: hard traces (call trace + returned-summary
quote), entry hard gate, STOP precheck and per-lane product gate, gate-trust
continuation (swallow ban / anchor mutants).

**V2.022** — Gate trust: no-subagent review endorsement, gates with red
baselines on real data and abstaining shadows, brief-and-audit quota.

**V2.021** — Upstream alignment: 25→27 sub-skills (added
implement-spec/pr/retro, dropped resolving-merge-conflicts), CONTEXT renamed
GLOSSARY.

**V2.020** — Trigger audit: roll-call trace check, file-state counting,
evidence-to-repo / log-to-logbook.

**V2.019** — Load discipline: roll-call invocation, per-lane reading,
single-round marker exemption.

**V2.018** — Continuous grilling: frontier-empty opening, six mid-lane hard
gates, bare grilling only mid-lane.

**V2.017** — Evidence discipline: receipt reconciliation, single benchmark
source, calibrated thresholds, control experiments.

**V2.016** — Round boundaries: understanding without edits, freshness
heartbeat, version self-check.

**V2.015** — Logbook diet + T0 truth: watermark-tail reads, ask-matt is a map
not a judge.

**V2.014** — Rename mattpocock-skills → autopilot (zero rule changes).

**V2.013** — Version handoff packet for cross-harness moves.

**V2.012** — Author alignment: grill→prototype exit, full triage suite, frozen
specs.

**V2.011** — Destructive guard: file-level red-phase backup, negative
evidence, marker counters.

**V2.010** — Official alignment: setup state bit, grill steering, prototype
gate, orchestration iron rule.

**V2.009** — Long-task hardening: frozen spec baseline, four closing audits,
tdd-n/a marking, steady heartbeat.

**V2.008** — Field distillation from 20 task entries + 3 driver reflections.
Self-scan checklist extended (green-lock question after red→green; forced
slowdown after 3 consecutive failures; same-file regression smoke; design-fork
nudge toward codebase-design). No-harness expected values must cite an
independent truth source, with at least one guard assertion differing from the
buggy output. Test-registry discipline (one unified entry, every test
registered, costly tests tiered). External review handling (reproduce → fix →
reply with red/green evidence). Adopted field remedies (shell-append for the
logbook, NOTES as JOURNAL fallback, Edit-tool over scripted replace,
Windows/MSYS notes). B-vs-D routing contradiction pinned: user-reported bugs
always take the diagnosis lane; Gate 0 gains a BROKEN exit; non-git
code-review fast-track made explicit.

**V2.007** — Scheduled reflection. Every 3 engineering rounds, after task
close, the driver appends a reflection entry to the central logbook: fixed
goal preamble + five evidence-based questions (invocation timing / vague
rules / self-invented workarounds / biggest gap to the goal / other). Counting
is tolerant by design; reflections only ever land in the logbook.

**V2.006** — Utilization & continuity, hardened by six real field runs.
Real-skill-first (bundled fallbacks only for uninstalled skills; skipping the
real skill = logged deviation). Task-needed external facts go through the
research form (background agent + cited notes). 15-second mid-execution
self-scan of core triggers. Same-session continuity (full re-read only at
session start / after compact / when unsure). WORKFLOW-ACTIVE marker plus a
standing AGENTS.md hook so a fresh window re-invokes the driver itself. Setup
must precede the first code-touching round. User policy codified: spend
tokens before asking a human — review and verify are never exempted.

**V2.005** — Eval-hardened against three plain-language test prompts (a broken
toggle, a copy-time button, a vague project idea). Chinese short requests
trigger directly; symptom text alone satisfies the bug-lane entry;
pure-understanding tasks enter no lane; doc-only sub-skill replies are
executed inline with a noted substitution; no-verify repos invent a seam
assert + smoke.

**V2.004** — Logging is part of task close, not user-prompted: one entry per
task (delivered/STOP/BLOCKED) in the central logbook; cross-round tasks log
once at close; no-skill rounds note the reason. Task-vs-round semantics
pinned.

**V2.003** — Central logbook: one shared file (location chosen by the
installer), 5-aspect entries (what happened / why each skill fired / friction
/ missed-skill self-check / result), append-only, never inside the skill
package.

**V2.002** — Single-trigger full autopilot: cross-round self-bootstrap, 8 core
skills with entry conditions + deliverable contracts (rest via a
four-question template), delivery gate for non-coders (one-sentence summary +
hand-check list + pasted verify output), HTML dashboard dropped, light trace
files, friction-only logging, self-evolution gate (propose only, never
self-edit).

**V2.001** — Baseline: the slimmed driver (trigger table + resume rules,
history archived, rule details split into `references/`).
