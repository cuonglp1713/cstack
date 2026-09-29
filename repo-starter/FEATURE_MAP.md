# Product feature map

No user-facing feature exists yet. Add a row after the first runnable vertical slice; do not invent screens, routes, selectors, or commands from a plan. Keep the map from the user's point of view so an agent can find and verify a reported problem.

| User journey | Entry point and action | Owning code | Observable proof | Gotchas |
|---|---|---|---|---|

For a web app, name navigation path and stable selectors. For an API, name method/path, authentication, and visible response. For a CLI, name the command and files/output it changes. For background work, include how the user starts it and sees completion. Update the affected row whenever an entry point, owning module, or proof path changes.
