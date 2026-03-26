# Skills

Skills are reusable instruction packs that agents load when a task matches a known artifact type or capability.

They are narrower than agents: a skill usually helps create one artifact type or perform one focused class of interaction.

## Included skills

### `record-story`

Creates a story artifact when the work is clear enough to become actionable.

- Saves to `work/backlog/backlog/`
- Uses a fixed story structure with title, type, context, requirements, and acceptance criteria

### `record-idea`

Records exploratory concepts and improvement ideas when the work is not ready to become a story.

- Supports both single-idea files and grouped themed idea files
- Saves to `work/ideas/ideas/`

### `record-guideline`

Records a compact guideline and updates project configuration so the new rule becomes part of the repo's operating context.

- Saves to `work/guidelines/`
- Also updates `work/project-config.md` so the guideline can be loaded later

### `record-adr`

Records an Architecture Decision Record using the required structure and naming convention.

- Saves to `work/adr/`
- Uses a date-based filename and standard ADR sections

### `agent-browser`

Provides the standard browser automation harness for browser-driven tasks such as inspecting pages, interacting with UI, and collecting evidence.

- Exposes a CLI workflow of open, snapshot, interact, and re-snapshot
- Supports screenshots, PDFs, state persistence, and multi-session usage

For the workflow roles that load these skills, see `docs/agents.md`.
