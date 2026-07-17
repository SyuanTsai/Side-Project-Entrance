# Requirements Coordinator

This folder contains the routing data used by
`requirements-coordinator-agent`.

The design avoids reading every service `README.md` on every request. Instead,
the agent should use these lightweight indexes first, then read only the
minimum required files for candidate services.

## Files

- `service-index.yml`: Workspace-level routing table for services and repos.
- `contract-registry.yml`: Workspace-level registry of shared contracts.
- `service-manifest.template.yml`: Optional per-service manifest template.

## Recommended Per-Service File

Each service can optionally add this file at its own root:

```text
.requirements-agent.yml
```

That file should describe the service's responsibility boundary, dependencies,
contracts, and requirement document entrypoints. It lets the coordinator avoid
falling back to broad README scans.

## Refresh Strategy

Update the index when:

- A new service or repo is added.
- A service changes ownership of a domain concept or data entity.
- A service adds, removes, or changes an API.
- A service adds, removes, or changes an event.
- Requirement document locations change.
- A shared contract changes.

For normal requirement work, prefer routing through the existing index and
registry rather than rebuilding them.
