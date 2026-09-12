# statekeeper

`statekeeper` is an agent skill for durable implementation tasks, append-only audit events, and advisory multi-agent coordination through Git branches and worktrees.

## Capabilities

- Multiple active objectives, each with a stable UUID and task file
- Durable current state under `.agent/statekeeper/tasks/`
- Immutable event files under `.agent/statekeeper/events/`
- Causal reconciliation through event predecessors
- Advisory claims for coordinating agents across Git worktrees
- Completed and abandoned task retention

Git is the transport and history layer, not a lock service. Claims cannot guarantee exclusion before commits are shared, fetched, and merged. Repository reality and current instructions always take precedence over recorded state.

## Install

Install with the Agent Skills installer:

```bash
npx skills add Infinity-002/statekeeper
```

The installer discovers `statekeeper` and lets you choose any supported agent harness and project or global scope.

For manual installation, place `SKILL.md` in a directory named `statekeeper` inside the harness's skills or user projects directory:

```text
<project-skills-dir>/statekeeper/SKILL.md
<user-skills-dir>/statekeeper/SKILL.md
~/.agents/skills/statekeeper/SKILL.md
~/.claude/skills/statekeeper/SKILL.md
```

The folder name must match the `name: statekeeper` frontmatter. Restart the harness after installation or changes if it loads skills only at startup.

## Repository State

```text
.agent/statekeeper/
  tasks/<task-id>.md
  events/<task-id>/<event-id>.md
```

Event files are authoritative and append-only. Task files are mutable current projections. Both are intended to be committed with the implementation they describe.
