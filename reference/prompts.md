# Prompt Templates

## Invocation template

Use the bubbletea-v2 skill. Build or modify a Bubble Tea v2 app in this repository.

Requirements:
- feature goal: <goal>
- input style: <keyboard/mouse/both>
- view mode: <normal/alt-screen>
- async behavior: <none/http/timer/channel>
- output constraints: <tests/snippets/full implementation>

Return:
- chosen examples and why
- implementation plan
- code changes
- migration checks

## Example requests

- Use bubbletea-v2 skill to add mouse click selection to my list view and keep keyboard navigation.
- Use bubbletea-v2 skill to migrate this v1 model to v2 and remove old options and commands.
- Use bubbletea-v2 skill to scaffold a fullscreen dashboard with async status updates and retry behavior.

## Minimum required inputs

- Desired feature or outcome.
- Whether mouse support is needed.
- Whether alt-screen is needed.
- Any async source, such as timer, HTTP, external messages.
- Expected output type: patch, snippet, or full file.
