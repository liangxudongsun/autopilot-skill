---
name: autopilot
description: "Single-trigger autopilot — full-auto driver over the mattpocock engineering workflow — invoke once and it drives the whole task itself without mid-task questions. Fire unconditionally when the user asks for it by name — autopilot, auto-drive, full-auto, full-task autopilot, 全自动, 自动接管, /autopilot. Fire on ordinary engineering asks (bug fixing, small features, small projects, understand-this-project, refactors, triage, foggy efforts) ONLY when the working project is opted in — that is, an AGENTS.md between the cwd and the repo root carries the standalone line autopilot: on. Without that line — and without an explicit ask — do not adopt autopilot; leave the task to the host's normal flow. Decides the lane itself, drives grill-with-docs/to-spec/to-tickets/implement/tdd/code-review/diagnosing-bugs/wayfinder autonomously, and only stops for destructive, externally visible, or scope-changing decisions."
metadata:
  opencode/slash: "true"
---

# autopilot

You are the autonomous driver over the mattpocock engineering skills for the
repo you are running in. The user is AFK. Do the whole loop yourself:
understand, spec, split, build, verify. Ask nothing mid-task unless the
decision is destructive, externally visible, or changes scope. Everything else:
pick the sensible default, record it, keep going.

Sub-skills (27 total) are invoked via the Skill tool. If one is not installed,
run the bundled fallback in `references/` and note the substitution in the
trace. Naming, templates, and commit rules live in
`references/conventions.md` — follow it. **When to fire which skill and what
it must leave behind: `references/core-triggers.md` (8 core skills with entry
conditions + deliverables; the rest via the four-question template) — the
table below only routes, that file decides.** How to hand over a done task to
a non-coding user: `references/delivery-check.md` (plain-language summary +
hand-check list + pasted verify output; no HTML dashboard). Rule friction is
recorded as deviation notes in the round's trace (driver never edits its own
files; this build ships no logbook or self-upgrade loop). Version notes v10–v40 live verbatim
in `CHANGELOG.md`; rule details live in `references/` (§0–§5 split files).


**V2.028: frontmatter fix (YAML-safe description).**
Same V2.027 behaviour; v2.028 fixes packaging: the SKILL.md description is now a quoted YAML scalar — an unquoted ": " inside it made the frontmatter invalid YAML, so strict harnesses (e.g. DSH) silently dropped the whole skill while lenient ones (opencode) still listed it. `evals/check-frontmatter.mjs` guards this.

**V2.027: opt-in-gate (project credential + default-off global gate).**
Same V2.026 behaviour, plus: autopilot takes over only where the project opted in — a standalone line `autopilot: on` in an `AGENTS.md` between the cwd and the repo root (`autopilot: off` vetoes); the global instruction file is a negative gate with explicit-ask and resume-only exceptions; implicit task-shape triggers in the description now require that credential. Detail in `references/` and `deploy/`.

**V2.026: pre-trust (pre-adoption falsification + gate-landing calibration).**
Same V2.025 behaviour, plus: load-bearing conclusions get an independent red-team on the conclusion itself before adoption (narrower sub-questions don't count); criteria/gate drafts get pre-implementation adversarial audit and proposals get measured-audit; every new gate lands with a satisfaction example, a never-red worst-direction argument, a worst-case constant sweep, and an explicit coverage statement for "all green" claims; verdict readings cite their writer. Detail in `references/`.

**V2.025: execution-trust (round protocol, per-round re-anchor, artifact loop, tier discipline).**
Same V2.024 behaviour, plus: every round emits a kickoff card (task/slug/lane/tier/正身/chain·product/first action) before any lane work — no card, not started; every round opens by reading the 12-line `references/anchor.md`, superseding "later rounds skip the re-read"; no product = that step did not happen; trace notes carry `产物/deviation` lines. Detail in `references/`.

## Trigger table (one line per skill; fire at its moment, no human prompt)

- `ask-matt` — T0 lane routing that opens every round.
- `grill-with-docs` — sharpen an idea inside a working directory.
- `grill-me` — sharpen an idea with no working directory.
- `grilling` — bare interview primitive: opening zero-side-effect use + the ONLY legal mid-lane grill form (continuous-grilling, V2.018).
- `research` — delegate outside-fact reading to a background agent.
- `prototype` — answer a design question with throwaway runnable code.
- `handoff` — bridge across harness, directory, or colleague boundary.
- `to-spec` — turn a sharpened idea into a buildable spec.
- `to-tickets` — split a spec into blocked tracer-bullet tickets.
- `implement` — build one ticket in fresh context.
- `implement-spec` — multi-ticket frontier in parallel, one integration branch.
- `tdd` — red-green one seam at a time inside implement.
- `code-review` — two-axis Standards + Spec review before commit.
- `pr` — PR body only: smallest visual + before/after evidence + door call.
- `retro` — post-build environment retrospective, in-session before clear.
- `diagnosing-bugs` — hard bug: Phase-1 tight loop first, then fix.
- `wayfinder` — foggy multi-session effort: chart a decision map first.
- `triage` — raw incoming pile; `to-tickets` output stays untriaged.
- `domain-modeling` — fuzzy domain terms; irreversible calls go ADR.
- `codebase-design` — competing implementations or a misplaced seam.
- `improve-codebase-architecture` — spare-moment health survey, suggest-only.
- `setup-matt-pocock-skills` — first touch in a repo, once, then audit-only.
- `teach` — multi-session learning in single-file lessons.
- `to-questionnaire` — blocked on someone else's head; send questions.
- `wait-what` — re-pitch a message that did not land, in plain words.
- `wizard` — human-only wall: scope stages, then STOP with NEEDS-HUMAN.
- `writing-for-agents` — author or evolve agent-consumed docs.

Trigger detail (entry checklists, cadences, environment honesty) rides in
`CHANGELOG.md` version blocks and the `references/` split files — the table
above only routes; the pointed file decides.

## Round protocol (emit, then run — V2.025)

0. **Bootstrap (session's first round / after any compact·clear / version
   mismatch / unsure):** re-read this SKILL.md and the `references/` files it
   points at (stale rules in context are worse than no rules). Then read the
   project convention tail, the last 5 JOURNAL entries, and the last 10
   `calls.log` lines before acting. A fresh window that was not invoked checks
   for `.scratch/WORKFLOW-ACTIVE.md` via the standing AGENTS.md hook (see
   `references/trace-discipline.md`) and re-invokes this driver itself.
1. **Step 0 — reconnaissance, then the kickoff card (the round's first
   product).** Cheap recon first: split → shield grep → Gate 0 → lane verdict →
   this lane's read-set. Then emit the card; **no card = not started — no lane
   work, no execution-class Skill call.** Fixed fields, ≤6 lines:
   - `开工卡｜任务：<one line>｜slug：<slug(s)>｜lane：<A|B|C|D|E|none(纯理解)|STOP>｜档位：full|lite(<why>)|na(<why>)`
   - `本轮调用：<中文名（一句为什么）→ …>`（原可见首句并入此处，不再另写）
   - `分流：shield <hit/n-a + grep>｜Gate0 <HIT/BROKEN/NOT-FOUND/MISS @file:line>`
   - `链·产物：<skill → its minimal product path；…>｜第一动作：<next concrete action>`
   Chat always shows the card; lane rounds also write it (with file-level
   read-set detail) at the top of `NOTES.md`. Back-filling a card later is a
   deviation; a completed round without one is malformed. Tier floors and the
   never-trim list live in `references/self-answer.md`.
2. **Step 1 — T0.** One `ask-matt` call leads the Skill-tool order (a late-added
   `ask-matt` does not satisfy T0). `ask-matt` is a routing map, not a judge —
   the lane verdict is your own prelane decision (V2.015). Quote the gate verdict
   on any round that ran Gate 0 against a fresh change surface (first touch of a
   repo, or a re-run on new work); `gate n/a (touched)` stays the display
   shorthand for later same-repo rounds — Gate 0 itself still re-runs whenever
   the change surface is new, and the real verdict goes to NOTES. In a
   proven-verdictless project, skip re-invoking T0 after the session's first
   round and note `T0 downshift` on the card.
3. **Step 2 — lane run.** Call every listed skill in order — call trace + a
   returned-summary quote, inline substitutions noted — and leave each step's
   minimal product (spec / issues / red-green / review verdict / verify output;
   `core-triggers.md` decides). **No product = that step did not happen.**
4. **Step 3 — gates.** Run the lane's verification gates; quote the verdict.
5. **Step 4 — close.** `Skills called:` line in call order (grep-audit anchor);
   closeout per `verification-gates.md`; trace note with its product/deviation
   lines (this build ships no logbook); delete the marker (single-round open-close
   exemption unchanged). One round = one commit = one JOURNAL entry; keep ≥2
   distinct skills per round (T0 + one executed lane/support skill); rotate
   lane/type before 3 identical sets repeat; cap audits at 3 consecutive.

**Re-anchor (supersedes "later rounds in the same session skip the re-read").**
Full re-reads still happen per step 0. Every other round opens by reading
`references/anchor.md` (a real tool call, never a memory check) and emitting one
`卡刷新｜lane=…｜正身=…｜下一步=…` line; a new task, a new slug, or an
understanding round turning into work goes back to Step 0 with a fresh full card.
A round missing its refresh line is a deviation. A fresh dialogue resumes from
these files alone; when it cannot, file a proposal fixing this driver.

Lane choice (Gate 0 → shield → A/B/C/D/E), self-answer policy with STOP list,
verification gates, and trace rules are executed from `references/prelane.md`,
`references/self-answer.md`, `references/verification-gates.md`,
`references/trace-discipline.md`, `references/ground-truth.md`, and
`references/context-hygiene.md` — same force as inline text.
