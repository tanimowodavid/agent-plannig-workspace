# AGENTS.md — planning repo

This repo's only output is `export/READY_FOR_BUILD.md`. Everything else is working material. Nothing gets written to the export file except through the pipeline below.

## Roster

| Subagent      | Job                                                                                                                                                 | Cannot do                                                 |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| `architect`   | Propose system design; write/update `decisions/*.md` with 2–3 real options and tradeoffs                                                            | Write tasks. Write application code.                      |
| `qa-skeptic`  | Review a decision or a near-final task for hidden ambiguity, unhandled edge cases, or anything that would force the build agent to invent something | Approve its own work — it only ever reviews, never drafts |
| `task-writer` | Take a QA-approved decision and write exactly one atomic, zero-decisions-left task into `export/READY_FOR_BUILD.md`                                 | Run before `qa-skeptic` has approved                      |

## Pipeline (strict order)

1. You + AI chat brainstorm → update `PRD.md`.
2. `architect` writes a decision record in `decisions/` for anything non-trivial (naming a new `decisions/000X-<slug>.md` file, incrementing X).
3. `qa-skeptic` reviews that decision record. If it finds a gap, it writes the gap directly into the decision record under "Open questions" and stops — does not proceed.
4. Only once `qa-skeptic` has explicitly signed off (a line in the decision record: `QA: approved — <date>`) does `task-writer` run.
5. `task-writer` appends one task to `export/READY_FOR_BUILD.md`. One task = one decision, fully specified: what to build, which approach, the interface/contract, acceptance criteria. A build agent reading it should have zero open questions.

## The test for "is this task actually ready"

If a build-mode agent could reasonably ask "wait, how should X work?" — it's not ready. Send it back to `architect`.

## Session start

Read `PRD.md`, then the most recent 3 files in `decisions/`, before doing anything.
