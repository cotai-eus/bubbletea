# Anti-Patterns and Corrections

1. Old pattern
- View returns string.
- Why wrong in v2: Model interface requires View() tea.View.
- Correct pattern: return tea.NewView(content) or build tea.View.

2. Old pattern
- Handle keys as tea.KeyMsg struct only.
- Why wrong in v2: key events split with interface model and dedicated press/release semantics.
- Correct pattern: use tea.KeyPressMsg for standard handling.

3. Old pattern
- Use msg.Type, msg.Runes, msg.Alt.
- Why wrong in v2: fields changed.
- Correct pattern: msg.Code, msg.Text, msg.Mod.Contains(tea.ModAlt).

4. Old pattern
- Match space as " ".
- Why wrong in v2: String now emits "space".
- Correct pattern: case "space".

5. Old pattern
- Use tea.MouseButtonLeft and related names.
- Why wrong in v2: constants renamed.
- Correct pattern: tea.MouseLeft, tea.MouseWheelUp, others in v2.

6. Old pattern
- Access mouse coords directly on old mouse struct.
- Why wrong in v2: mouse msg is interface.
- Correct pattern: msg.Mouse().X and msg.Mouse().Y.

7. Old pattern
- Use WithAltScreen and WithMouse options as primary control path.
- Why wrong in v2: terminal features moved to View declaration.
- Correct pattern: set fields in View each render.

8. Old pattern
- Use EnterAltScreen and ExitAltScreen commands.
- Why wrong in v2: removed command model for screen mode.
- Correct pattern: set View.AltScreen true and false.

9. Old pattern
- Use tea.Sequentially.
- Why wrong in v2: renamed and deprecated behavior path.
- Correct pattern: tea.Sequence.

10. Old pattern
- Use tea.WindowSize as Cmd.
- Why wrong in v2: RequestWindowSize is the v2 path.
- Correct pattern: tea.RequestWindowSize.

11. Old pattern
- Treat paste as key flag.
- Why wrong in v2: dedicated paste messages exist.
- Correct pattern: tea.PasteMsg, tea.PasteStartMsg, tea.PasteEndMsg.

Migration source of truth:
- [UPGRADE_GUIDE_V2.md](../../../../UPGRADE_GUIDE_V2.md)
