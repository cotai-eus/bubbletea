# Canonical Bubble Tea v2 Patterns in this Repository

## Model structure

- Keep mutable app state in model struct.
- Implement Init, Update, View.
- Use custom Msg types for async results and errors.

```go
package main

import (
    "fmt"
    "os"

    tea "charm.land/bubbletea/v2"
)

type model struct {
    count int
    err   error
}

type loadedMsg struct{ count int }
type errMsg struct{ err error }

func (m model) Init() tea.Cmd {
    return nil
}

func (m model) Update(msg tea.Msg) (tea.Model, tea.Cmd) {
    switch msg := msg.(type) {
    case tea.KeyPressMsg:
        switch msg.String() {
        case "q", "ctrl+c":
            return m, tea.Quit
        case "space":
            m.count++
        }
    case loadedMsg:
        m.count = msg.count
    case errMsg:
        m.err = msg.err
    }
    return m, nil
}

func (m model) View() tea.View {
    text := fmt.Sprintf("Count: %d\nPress space. q to quit.\n", m.count)
    if m.err != nil {
        text = fmt.Sprintf("Error: %v\n", m.err)
    }
    return tea.NewView(text)
}

func main() {
    if _, err := tea.NewProgram(model{}).Run(); err != nil {
        fmt.Fprintln(os.Stderr, err)
        os.Exit(1)
    }
}
```

## Init/Update/View flow

- Init returns first Cmd or nil.
- Update handles all Msg and returns next Cmd.
- View returns declarative tea.View, not string.

## Keyboard messages (v2)

- Prefer tea.KeyPressMsg for key handling.
- String matching for common keys; field matching for precision.
- Space key string is "space".

```go
case tea.KeyPressMsg:
    switch msg.String() {
    case "q", "ctrl+c":
        return m, tea.Quit
    case "space":
        // handle
    }

if msg.Code == 'c' && msg.Mod.Contains(tea.ModCtrl) {
    return m, tea.Quit
}
```

## Mouse messages (v2)

- tea.MouseMsg is interface; call msg.Mouse().
- Use specific message types for click/release/wheel/motion.

```go
case tea.MouseClickMsg:
    if msg.Button == tea.MouseLeft {
        // click behavior
    }
case tea.MouseWheelMsg:
    if msg.Button == tea.MouseWheelUp {
        // scroll up behavior
    }
case tea.MouseMsg:
    mouse := msg.Mouse()
    _ = mouse.X
    _ = mouse.Y
```

## Asynchronous commands

- Cmd is func() Msg.
- Use tea.Batch for concurrent commands.
- Use tea.Sequence for ordered commands.
- Use tea.Tick and tea.Every for recurring updates.

```go
func fetchCmd() tea.Msg {
    return loadedMsg{count: 42}
}

func tickCmd() tea.Cmd {
    return tea.Tick(time.Second, func(t time.Time) tea.Msg {
        return loadedMsg{count: int(t.Unix() % 100)}
    })
}

func (m model) Init() tea.Cmd {
    return tea.Batch(fetchCmd, tickCmd())
}
```

## Composition patterns

- Keep sub-models inside parent model.
- Route Msg to each sub-model Update.
- Compose final screen in one View.

## Declarative View fields to prefer

- AltScreen
- MouseMode
- ReportFocus
- DisableBracketedPasteMode
- WindowTitle
- Cursor
- ForegroundColor and BackgroundColor
- KeyboardEnhancements
- ProgressBar
- OnMouse

## Evidence

- [UPGRADE_GUIDE_V2.md](../../../../UPGRADE_GUIDE_V2.md)
- [tea.go](../../../../tea.go)
- [key.go](../../../../key.go)
- [mouse.go](../../../../mouse.go)
- [commands.go](../../../../commands.go)
