# _(project-name)_-planning

This repo is where the project gets **thought**, not built. It contains almost no application code — just the PRD, the system design, decision records, and a pipeline that turns finalized decisions into build-ready tasks for the actual codebase.

## Why a separate repo

A build agent should never have to invent an architecture decision mid-task. This repo is the gate: nothing becomes a task in the build repo until it's been designed here and survived QA review here.

## How to use this as a GitHub template

1. On GitHub, go to this repo's **Settings → Template repository** and check the box.
2. For every new project: click **Use this template** → gives you a clean copy, no manual cloning/renaming.
3. Fill in `PRD.md`, then start using the subagents below.

## The pipeline

```
  brainstorm w/ AI chat
        │
        ▼
   PRD.md (what & why)
        │
        ▼
  architect subagent  ──►  decisions/000X-*.md  (how, + alternatives considered)
        │
        ▼
  qa-skeptic subagent ──►  pokes holes; blocks until the decision has zero
        │                  remaining ambiguity
        ▼ (approved)
  task-writer subagent ──► appends one atomic task to export/READY_FOR_BUILD.md
        │
        ▼
  you copy/paste that task into the BUILD repo's TASKS.md
```

## Repo structure

- `PRD.md` — what you're building and why. The vision doc.
- `decisions/` — one file per architectural decision (ADR-style). Permanent record of _why_, so you never have to re-litigate a choice.
- `export/READY_FOR_BUILD.md` — staging area. Only fully-QA'd, zero-ambiguity tasks land here. This is the only file that should ever leave this repo.
- `.claude/agents/` — the subagent roster (architect, qa-skeptic, task-writer).
- `AGENTS.md` — instructions for whichever agent/tool is working in this repo.
