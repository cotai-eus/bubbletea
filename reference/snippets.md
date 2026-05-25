# Reusable Snippets

## Error message type pattern

```go
type errMsg struct{ err error }

func loadCmd() tea.Msg {
    if err := doWork(); err != nil {
        return errMsg{err: err}
    }
    return doneMsg{}
}
```

## Sequence and Batch composition

```go
return m, tea.Sequence(
    stepOneCmd,
    tea.Batch(stepTwoACmd, stepTwoBCmd),
    stepThreeCmd,
)
```

## Request and handle window size

```go
func (m model) Init() tea.Cmd {
    return tea.RequestWindowSize
}

case tea.WindowSizeMsg:
    m.width = msg.Width
    m.height = msg.Height
```

## Focus and blur support

```go
case tea.FocusMsg:
    m.focused = true
case tea.BlurMsg:
    m.focused = false

v.ReportFocus = true
```

## Mouse message extraction

```go
case tea.MouseMsg:
    mouse := msg.Mouse()
    m.lastX = mouse.X
    m.lastY = mouse.Y
```

## Paste message handling

```go
case tea.PasteStartMsg:
    m.pasting = true
case tea.PasteMsg:
    m.buf += msg.Content
case tea.PasteEndMsg:
    m.pasting = false
```
