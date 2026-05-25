# Operational Checklists

## New app creation checklist

- Confirm import path uses charm.land/bubbletea/v2.
- Define model struct with explicit state fields.
- Implement Init, Update, View signatures exactly.
- Ensure View returns tea.View.
- Use tea.KeyPressMsg and v2 key names.
- Use custom Msg for async outcomes and errors.
- Prefer declarative View fields for terminal behavior.
- Add quit keys: q and ctrl+c.
- Handle WindowSizeMsg if layout depends on terminal dimensions.
- Add at least one test path for non-trivial update flow.

## PR review checklist

- Any v1 APIs present, including old mouse constants or View string.
- Async commands returned correctly.
- Msg types explicit for success and error branches.
- View declaratively represents terminal behavior.
- Key handling robust with String or field checks.
- Mouse handling uses v2 msg interfaces and types.
- Sequence vs Batch intent is explicit.
- Exit and error states render clearly.

## v1 to v2 migration checklist

- Update import paths to charm.land/bubbletea/v2.
- Change View signature from string to tea.View.
- Replace tea.KeyMsg struct usage with tea.KeyPressMsg handling.
- Replace msg.Type and msg.Runes and msg.Alt with v2 fields.
- Replace case " " with case "space".
- Replace old mouse constants and coord access patterns.
- Move old options and commands to declarative View fields.
- Replace tea.Sequentially with tea.Sequence.
- Replace tea.WindowSize with tea.RequestWindowSize.
- Replace paste key-flag assumptions with paste messages.
