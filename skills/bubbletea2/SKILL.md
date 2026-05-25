# Bubbletea TUI Development

Production-ready skill for building, reviewing, and migrating TUI applications with Go, Bubble Tea v2, and Lip Gloss, using local references from this repository.

## When to use this skill

Use this skill when the task involves one or more of the following:

- Building a new TUI with `Init/Update/View` architecture
- Adding Bubble Tea/Bubbles components to an existing app
- Fixing layout bugs (width, height, border, overflow, line wrapping)
- Implementing keyboard, mouse, focus, or paste interaction
- Migrating Bubble Tea v1 code to v2
- Reviewing TUI PRs with focus on bugs and behavioral regressions

## When not to use

- Changes that do not involve TUI or Bubble Tea
- Refactoring only presentation without functional impact
- Web frontend tasks outside terminal UI

## Required local references

Before proposing a solution, consult:

- `reference/README.md`
- `reference/canonical-patterns.md`
- `reference/anti-patterns.md`
- `reference/checklists.md`
- `reference/troubleshooting.md`
- `reference/recipes.md`
- `reference/snippets.md`
- `reference/examples/README.md`

## Hard gates (required sequence)

Advance only after each gate is satisfied:

1. Gate A - Scope correctness
  - Confirm the request is for Bubble Tea TUI and identify the task type: `build`, `migrate`, `debug`, or `review`.

2. Gate B - Local evidence
  - Every technical decision cites at least one file from `reference/` or `reference/examples/`.
  - No recommendation should rely only on implicit memory.

3. Gate C - v2 anti-regression
  - Verify key v1 anti-patterns: `View() string`, legacy key handling, old mouse constants, incorrect `Batch` vs `Sequence` usage.

4. Gate D - Behavioral evidence
  - For bugs or reviews, each finding must include objective evidence (file + line or short snippet) and concrete risk.

5. Gate E - Final checklist
  - Run the applicable checklist (`new app`, `review`, or `migration`) before concluding.

## Core principles

- Canonical architecture: state in the `model`, flow through messages, async commands via `tea.Cmd`
- `View()` must always return `tea.View` in v2
- Interactions should be declarative and predictable
- Keyboard and mouse should use v2 APIs (`tea.KeyPressMsg`, `tea.Mouse*Msg`)
- Async work should not block the update loop
- Final output should be action-oriented: what changed, why, and how to validate

## Recommended workflow

1. Classify the request
  - `build`: new feature/component
  - `migrate`: v1 -> v2 adaptation
  - `debug`: bug fix with reproduction/root cause
  - `review`: risk and regression analysis

2. Map the base pattern
  - Find the pattern in `reference/canonical-patterns.md`
  - Select an example in `reference/examples/README.md`

3. Implement or review
  - Apply the smallest possible set of changes
  - Preserve public APIs when no change is required

4. Validate
  - Check `reference/checklists.md`
  - If an issue recurs, consult `reference/troubleshooting.md`

5. Respond
- Deliver technical decisions + evidence + next objective steps

## Review mode (high priority)

When the request is a review, respond in this order:

1. Findings by severity (`Critical`, `Major`, `Minor`)
2. Evidence for each finding (file/line or snippet)
3. Expected behavioral risk
4. Suggested fix with minimal impact
5. Then: short summary

If no relevant findings exist, state explicitly that no critical bugs were discovered and note residual risks (e.g. insufficient test coverage).

## Quick decision heuristics

- Use `tea.Sequence` when order dependency exists
- Use `tea.Batch` when commands are independent
- If layout depends on terminal size, consider `tea.RequestWindowSize`
- If input is inconsistent, validate `msg.String()` and `msg.Mod.Contains(...)`
- If mouse fails, verify the mode configuration in `View`

## Common issues to block

- `View()` returning `string` in Bubble Tea v2
- Blocking execution inside `Update`
- Incorrect space key match (`" "` instead of `"space"`)
- Using v1 keyboard/mouse APIs in v2 code
- Fixes without reproduction proof or final validation

## Catalog of the 63 examples

All examples below are indexed in `reference/examples/README.md`. Descriptions are concise and aligned with the example index.

- altscreen-toggle: Switches between main and alt-screen declaratively.
- autocomplete: Input with suggestions and term completion.
- canvas: Pixelated drawing and animation in a buffer.
- capability: Queries terminal capabilities at runtime.
- cellbuffer: Manipulates cell buffer for custom rendering.
- chat: TUI chat example with message flow.
- clickable: Clickable elements with mouse feedback.
- colorprofile: Detects terminal color profile support.
- composable-views: Composes reusable subviews on one screen.
- cursor-style: Changes cursor style based on context.
- debounce: Prevents repeated events with input debounce.
- doom-fire: Renders Doom Fire effect in the terminal.
- dynamic-textarea: Textarea with dynamic height by content.
- exec: Executes external commands and shows output.
- eyes: Eye animation following interactions.
- file-picker: File browser with interactive selection.
- focus-blur: Handles focus and blur events.
- fullscreen: Toggles fullscreen using alt-screen.
- glamour: Renders formatted markdown with glamour.
- help: Help overlay with shortcuts and context.
- http: Fetches HTTP data asynchronously with states.
- isbn-form: ISBN form with immediate validation feedback.
- keyboard-enhancements: Enables advanced keyboard terminal features.
- list-default: Default Bubbles list with navigation.
- list-fancy: Styled list with visual customizations.
- list-simple: Minimal list for quick selection.
- mouse: Captures mouse motion, clicks, and wheel.
- package-manager: Manages package flow in a list.
- pager: Views long text with scrolling.
- paginator: Pages large collections with controls.
- pipe: Reads piped input and renders it.
- prevent-quit: Blocks accidental quit keys.
- print-key: Shows captured key for debugging.
- progress-animated: Continuously animated progress bar.
- progress-bar: Basic progress bar with percentage.
- progress-download: Simulates download progress and states.
- progress-static: Static progress without animation.
- query-term: Search terms with incremental filtering.
- realtime: Updates UI with real-time data.
- result: Shows a result screen after a flow.
- send-msg: Sends internal messages between components.
- sequence: Chains commands in deterministic order.
- set-terminal-color: Sets the terminal color during runtime.
- set-window-title: Sets the terminal window title.
- simple: Minimal Bubble Tea example.
- space: Space-themed animation in the terminal.
- spinner: Single spinner indicator for loading.
- spinners: Gallery of multiple spinners.
- splash: Initial splash screen with transition.
- split-editors: Two editors side by side.
- stopwatch: Stopwatch with start, pause, and reset.
- suspend: Suspends and resumes the program in terminal.
- table: Interactive table with navigation.
- table-resize: Resizable table with column adjustment.
- tabs: Tab navigation with content.
- textarea: Multiline input with controls.
- textinput: Simple text field with validation.
- textinputs: Multiple inputs with focus switching.
- timer: Countdown timer with ticks.
- tui-daemon-combo: Combines TUI with a daemon process.
- vanish: Text or element disappears with effect.
- views: Switches between different screen views.
- window-size: Reacts to window size changes.

## Skill invocation template

Use this template when invoking the skill explicitly:

"Use this skill from the repository for [goal].
Context:
- type: [build|migrate|debug|review]
- input: [keyboard|mouse|both]
- screen mode: [normal|alt-screen]
- async behavior: [none|timer|http|external-msg]
- expected output: [patch|snippet|full implementation]
Output:
- decisions made
- changes applied
- validations executed
- residual risks"

## Expected skill output

- Clear, executable technical recommendation
- Local references used to support decisions
- Minimal changes focused on the problem
- Final checklist applied