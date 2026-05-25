# Troubleshooting

1. Symptom: compile error on View method type.
- Diagnosis: View still returns string.
- Fix: change to View() tea.View and return tea.NewView.

2. Symptom: spacebar not triggering logic.
- Diagnosis: matching " " in key String.
- Fix: match "space".

3. Symptom: mouse events missing.
- Diagnosis: mouse mode not set in View.
- Fix: set v.MouseMode to MouseModeCellMotion or AllMotion.

4. Symptom: old mouse constants unresolved.
- Diagnosis: using v1 names.
- Fix: use tea.MouseLeft and wheel constants in v2.

5. Symptom: key modifier logic wrong.
- Diagnosis: strict equality on Mod with combined modifiers.
- Fix: use msg.Mod.Contains patterns.

6. Symptom: async task blocks UI.
- Diagnosis: task executed directly in Update.
- Fix: return Cmd and let runtime run it asynchronously.

7. Symptom: ordered steps run out of order.
- Diagnosis: used Batch where Sequence was required.
- Fix: use tea.Sequence.

8. Symptom: paste input not captured.
- Diagnosis: expecting paste inside key message.
- Fix: handle PasteStartMsg, PasteMsg, PasteEndMsg.

9. Symptom: focus events never fire.
- Diagnosis: focus reporting disabled.
- Fix: set v.ReportFocus true.

10. Symptom: terminal toggles not applying reliably.
- Diagnosis: imperative command mindset from v1.
- Fix: drive behavior from View fields each render.
