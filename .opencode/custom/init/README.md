# AiFact Flow

Artifact-based AI workflow for disciplined software delivery.

AiFact is a repo-local framework for using AI in software delivery without relying on hidden chat state. It keeps context, decisions, work state, and handoffs in repository artifacts so the workflow stays explicit, reviewable, and durable.

Repository: https://github.com/arminc/aifact

## Why it exists

Experienced engineers do not start each task from zero. They already know the repository structure, the local rules, the project history, the common failure modes, and what is still underspecified.

AI usually does not.

That gap is the reason AiFact exists. Instead of relying on a long chat, hidden memory, or prompt luck, AiFact puts the working context into repo artifacts so the model can operate with durable, reviewable context.

- project context lives in repo files
- work state lives in repo files
- reviews and decisions live in repo files
- handoffs happen through repo files

This makes AI-assisted delivery more auditable, more repeatable, and easier to maintain across sessions, contributors, and model upgrades.

## Core ideas

- Artifacts on disk are the source of truth.
- `work/` holds durable project context, story state, ideas, ADRs, and release artifacts.
- Agents have narrow roles with explicit handoffs instead of one general-purpose coding role doing everything.
- Validation is a gate, not a courtesy step.

## Why not just use a coding agent and a long chat?

That can work for small tasks, but it gets fragile when the work needs durable handoffs, repeatable validation, project-specific rules, and visible delivery history.

AiFact chooses a different tradeoff:

- artifacts instead of hidden state
- narrow roles instead of one giant role
- repo-local context instead of repeated prompt explanations
- validation as a gate instead of a suggestion
- visible delivery history instead of ephemeral chat memory

## How it works

The normal delivery path starts by clarifying the work, records that understanding in a story, then moves through analysis, implementation, validation, and closeout.

1. Start with `brainstorm` to clarify what should be built.
2. Record the result as a durable artifact with `record-story`.
3. Run delivery phases such as analysis, implementation, and validation against that artifact.
4. Close the loop with done-state and PR workflows after validation passes.

## What is in this repo

- `.opencode/` contains the workflow implementation: agents, commands, skills, scripts, and bootstrap assets.
- `work/` contains durable repo-local artifacts that guide AI behavior and preserve delivery history.
- `docs/` contains the detailed framework reference.

## Documentation

- `docs/overview.md` - framework concepts and rationale
- `docs/getting-started.md` - onboarding and first-run path
- `docs/workspace.md` - what `work/` is for and how it is structured
- `docs/agents.md` - agent roles and responsibilities
- `docs/commands.md` - command entry points
- `docs/skills.md` - reusable skills
- `docs/flows.md` - story flow, delivery loop, and artifact flow
- `docs/prompting.md` - prompt reference file notes

If you only remember one rule, remember this one: start with `brainstorm`, and treat the artifact on disk as the source of truth.
