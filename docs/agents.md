# Agents

Agents are the primary workflow roles. They are the conceptual center of AiFact.

Each agent has a narrow job, reads repo context before acting, and leaves a durable artifact or state change for the next phase instead of relying on chat memory.

## Core delivery agents

### `brainstorm`

The normal entry point for delivery work. It clarifies what should be built before implementation planning begins.

- Reads repo context first, especially `work/project-config.md`
- Stays in concept-refinement mode rather than implementing
- Can record docs and work artifacts under `work/`, `docs/`, and `.opencode/` when asked

### `story-reviewer`

Pressure-tests an existing story for hidden complexity, risky assumptions, unclear wording, and likely failure modes.

- Used after a story exists, not for first-pass ideation
- Challenges the draft rather than rewriting broad product intent

### `story-start`

Moves drafted work into active delivery and establishes the starting point for the rest of the flow.

- Accepts stories from `work/backlog/backlog/` or `work/backlog/planned/`
- Moves the story to `work/backlog/in-progress/`
- Creates or reuses the working branch and records the kickoff in git

### `story-analyzer`

Identifies where in the repo the story should be implemented and writes repo-grounded analysis into the story.

- Finds the primary implementation lane and likely adjacent touchpoints
- Adds or updates the `## Analysis` section in the story
- Optimizes for scoping implementation, not redesigning the feature

### `story-implementer`

Executes story-driven changes against the recorded analysis and repo-local rules.

- Requires `## Analysis` to exist before implementation starts
- Treats repo-configured commands as the verification source of truth
- Can use `story-builder` only for rare, clearly bounded execution slices

### `story-validator`

Acts as the release gate. It gathers proof and decides whether the story passes, fails, or is blocked.

- Turns the story into an explicit validation checklist
- Prefers the narrowest credible proof surface first
- Appends either `## Implementation feedback` or `## Validation update` to the story

### `story-done`

Closes validated work by moving the story into done state and preparing final closure.

- Requires a successful validation update before closeout
- Moves the story to `work/backlog/done/`
- Commits the completed story work when the staged scope is clean

### `story-pr`

Owns the pull request and CI follow-through phase.

- Creates or reuses the GitHub PR for the current branch
- Waits for checks through the repo-local wait script
- Allows limited recovery for CI-owned failures, but not broad product-code rework

## Supporting agents

### `story-builder`

A bounded helper that `story-implementer` can use for a rare separable slice. It is not a normal workflow phase.

- Used only when a slice has clear file boundaries and limited dependency edges
- Returns control to `story-implementer`, which still owns the story

### `browser-validator`

Handles browser-specific validation evidence when a story needs visible UI proof or focused E2E debugging.

- Covers only the browser-specific subset of validation
- Works alongside `story-validator`, not instead of it

### Orchestrators

- `story-execute-orchestrator` runs the story flow through validation
- `story-ship-orchestrator` runs the full story flow through closure and PR follow-through

These orchestrators re-read the story between phases and use the recorded artifact as the authority.

### Additional specialized agents

- `ad-hoc-implementer` for bounded changes that do not need a story
- `external-ideas-reviewer` for repo improvement review with vendor-neutral wording
- `lightweight-command-runner` for narrow fixed command flows

For the order these agents appear in delivery, see `docs/flows.md`.
