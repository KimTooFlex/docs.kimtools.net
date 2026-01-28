---
icon: circle-dot
---

# Radio

KimTools provides RadioBox and RadioButton for scenarios where a single option must be selected from a group.

Both controls inherit from the native WinForms RadioButton control. They share the same underlying Windows behavior, including mutual exclusivity, keyboard navigation, events, and accessibility support. Internally, they are the same engine. The difference is how they are presented and where they are best used.

[KtRadioBox](kt-radiobox.md) follows the traditional radio button appearance. It is suited for forms, dialogs, and settings pages where users select one option from a clearly defined group.

[KtRadioButton](radio-button.md) uses the same radio foundation but is styled to look and behave like a selectable button. When selected, it appears pressed, while other buttons in the same group are automatically released. This is useful for toolbars, segmented controls, and modern UIs that prefer button-style selection.

In short, both controls rely on the native WinForms radio button for correctness and consistency. KimTools exposes them in two visual forms so you can choose clarity or a more action-driven layout without changing selection logic.
