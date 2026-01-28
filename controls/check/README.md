---
icon: octagon-check
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# Check

KimTools provides two closely related controls: CheckBox and CheckButton. Both are designed to represent a boolean state while fitting different UI patterns.

At the core, both controls inherit from the native WinForms CheckBox button. This means they share the same underlying behavior, state handling, events, and accessibility support provided by Windows. The difference is not in how they work internally, but in how they are presented to the user.

[Check-Box](kt-checkbox.md) follows the traditional checkbox pattern. It is best suited for forms, settings pages, and option lists where users expect a familiar and clear interaction model.

[Check-Button](kt-checkbutton.md) uses the same checkbox foundation but is styled and configured to behave like a toggleable button. When clicked, it remains pressed to indicate the checked state and releases when unchecked. This makes it ideal for toolbars, action panels, and modern interfaces where a button-style toggle feels more natural.

In short, both controls share the same engine and reliability of the native WinForms checkbox. KimTools exposes them as two controls to give you visual flexibility without changing behavior.
