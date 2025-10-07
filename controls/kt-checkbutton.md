---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# 🔹 Kt-CheckButton&#x20;

### Overview

**KtCheckButton** is a modern, customizable toggle button control that combines the functionality of a checkbox with the visual appearance of a button. It provides rich styling options including gradients, icons, and smooth state transitions, making it ideal for creating engaging user interfaces in Windows Forms applications.

***

### Key Properties

| Property                | Type               | Default                              | Description                                                 |
| ----------------------- | ------------------ | ------------------------------------ | ----------------------------------------------------------- |
| **Checked**             | `bool`             | `false`                              | Gets or sets whether the button is in checked/toggled state |
| **Text**                | `string`           | `""`                                 | The text displayed on the button                            |
| **Icon**                | `string`           | `""`                                 | Icon identifier for unchecked state                         |
| **Icon\_Checked**       | `string`           | `"tabler.solid.circle_check_filled"` | Icon identifier for checked state                           |
| **Background**          | `KtBrush`          | `Gradient`                           | Background brush for unchecked state                        |
| **Background\_Checked** | `KtBrush`          | `Solid`                              | Background brush for checked state                          |
| **Border**              | `KtBrush`          | `Gradient`                           | Border brush for unchecked state                            |
| **Border\_Checked**     | `KtBrush`          | `Solid`                              | Border brush for checked state                              |
| **BorderRadius**        | `float`            | `10`                                 | Roundness of button corners                                 |
| **BorderWidth**         | `float`            | `2`                                  | Thickness of the border                                     |
| **Foreground**          | `KtColor`          | `Empty`                              | Text/icon color for unchecked state                         |
| **Foreground\_Checked** | `KtColor`          | `Empty`                              | Text/icon color for checked state                           |
| **IconSize**            | `int`              | `16`                                 | Size of the icon in pixels                                  |
| **IconStroke**          | `double`           | `2.5`                                | Stroke width for icon rendering                             |
| **TextAlign**           | `ContentAlignment` | `MiddleCenter`                       | Alignment of text within button                             |
| **ImageAlign**          | `ContentAlignment` | `MiddleLeft`                         | Alignment of icon within button                             |
| **TextMargin**          | `int`              | `0`                                  | Spacing between text and icon                               |
| **Padding**             | `Padding`          | `7,7,7,7`                            | Internal padding of button content                          |

***

### Events

| Event              | Description                               |
| ------------------ | ----------------------------------------- |
| **CheckedChanged** | Fires when the `Checked` property changes |

***

### Basic Usage

#### Simple Toggle Button

```csharp
var toggleButton = new KtCheckButton
{
    Text = "Enable Feature",
    Location = new Point(20, 20),
    Size = new Size(150, 40)
};

// Handle state changes
toggleButton.CheckedChanged += (s, e) =>
{
    var isChecked = toggleButton.Checked;
    MessageBox.Show($"Feature is now {(isChecked ? "enabled" : "disabled")}");
};

this.Controls.Add(toggleButton);
```

#### Button with Icon

```csharp
var iconButton = new KtCheckButton
{
    Text = "Dark Mode",
    Icon = "tabler.moon",
    Icon_Checked = "tabler.sun",
    IconSize = 20,
    TextAlign = ContentAlignment.MiddleCenter,
    ImageAlign = ContentAlignment.MiddleLeft,
    Size = new Size(140, 45)
};
```

***

### Styling Examples

#### Gradient Background

```csharp
var gradientButton = new KtCheckButton
{
    Text = "Premium",
    Background = new KtBrushGradient
    {
        StartColor = KtColor.PRIMARY,
        StopColor = KtColor.SECONDARY,
        Angle = 45
    },
    Background_Checked = new KtBrushGradient
    {
        StartColor = KtColor.SUCCESS,
        StopColor = KtColor.INFO,
        Angle = 45
    },
    BorderRadius = 15,
    Foreground = KtColor.WHITE
};
```

#### Solid Color with Custom Border

```csharp
var solidButton = new KtCheckButton
{
    Text = "Subscribe",
    Background = KtBrush.Solid,
    Background_Checked = KtBrush.Solid,
    Border = new KtBrushSolid { Color = KtColor.PRIMARY },
    Border_Checked = new KtBrushSolid { Color = KtColor.SUCCESS },
    BorderWidth = 3,
    BorderStyle = DashStyle.Solid,
    BorderRadius = 8
};
```

#### Minimalist Style

```csharp
var minimalButton = new KtCheckButton
{
    Text = "Option",
    Background = KtBrush.None,
    Border = KtBrush.None,
    Foreground = KtColor.BASE_CONTENT,
    Foreground_Checked = KtColor.PRIMARY,
    IconSize = 18,
    Icon = "tabler.circle",
    Icon_Checked = "tabler.circle_check"
};
```

***

### Advanced Features

#### Custom Icon Colors

```csharp
var customIconButton = new KtCheckButton
{
    Icon = "tabler.heart",
    Icon_Checked = "tabler.heart_filled",
    IconColor = KtColor.BASE_300,
    IconColor_Checked = KtColor.ERROR,
    IconSize = 24,
    IconStroke = 2.0
};
```

#### Text and Icon Alignment

```csharp
var alignedButton = new KtCheckButton
{
    Text = "Settings",
    Icon = "tabler.settings",
    TextAlign = ContentAlignment.MiddleRight,
    ImageAlign = ContentAlignment.MiddleLeft,
    TextMargin = 3,  // Spacing between icon and text
    Size = new Size(120, 40)
};
```

#### Programmatic Control

```csharp
// Toggle the button state
toggleButton.Checked = !toggleButton.Checked;

// Refresh appearance
toggleButton.Render();

// Suspend layout updates for batch changes
toggleButton.SuspendLayout();
toggleButton.Background = newBrush;
toggleButton.BorderRadius = 12;
toggleButton.ResumeLayout(true);
```

***

### Common Patterns

#### Toggle Group (Radio-like Behavior)

```csharp
var buttons = new[] 
{
    new KtCheckButton { Text = "Option 1", Tag = 0 },
    new KtCheckButton { Text = "Option 2", Tag = 1 },
    new KtCheckButton { Text = "Option 3", Tag = 2 }
};

foreach (var btn in buttons)
{
    btn.CheckedChanged += (s, e) =>
    {
        if (((KtCheckButton)s).Checked)
        {
            // Uncheck all others
            foreach (var other in buttons)
                if (other != s) other.Checked = false;
        }
    };
    
    this.Controls.Add(btn);
}
```

#### State Indicator

```csharp
var statusButton = new KtCheckButton
{
    Text = "Connected",
    Icon = "tabler.wifi",
    Icon_Checked = "tabler.wifi_off",
    Background_Checked = new KtBrushSolid { Color = KtColor.ERROR },
    Foreground_Checked = KtColor.WHITE,
    Enabled = false  // Display-only
};
```

#### Animated Theme Toggle

```csharp
var themeToggle = new KtCheckButton
{
    Icon = "tabler.moon",
    Icon_Checked = "tabler.sun",
    IconSize = 22,
    BorderRadius = 20,
    Size = new Size(50, 50)
};

themeToggle.CheckedChanged += (s, e) =>
{
    bool isDarkMode = themeToggle.Checked;
    ApplyTheme(isDarkMode);
};
```

***

### Design Tips

1. **Consistency**: Use the same `BorderRadius` across related buttons for visual cohesion
2. **Icon Selection**: Choose icons that clearly represent both states (e.g., play/pause, on/off)
3. **Color Contrast**: Ensure checked and unchecked states are visually distinct
4. **Hover Effects**: The control automatically provides hover feedback
5. **Accessibility**: The button defaults to a hand cursor to indicate interactivity

***

### Performance Notes

* Use `SuspendLayout()` and `ResumeLayout()` when making multiple property changes
* The `Render()` method is automatically called on property changes
* Icon rendering is cached for performance

***

### Related Controls

* [**KtCheckBox**](kt-checkbox.md): Traditional checkbox with advanced styling
