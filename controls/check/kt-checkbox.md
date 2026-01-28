---
icon: square-check
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

# CheckBox

### Overview

**KtCheckBox** is a highly customizable checkbox control that provides enhanced visual support for on/off states with smooth animations, multiple styles, and label binding capabilities. Inspired by modern checkbox designs, it offers rich state management and flexible styling options for Windows Forms applications.

***

### Key Properties

| Property                            | Type                      | Default    | Description                                                      |
| ----------------------------------- | ------------------------- | ---------- | ---------------------------------------------------------------- |
| **Checked**                         | `bool`                    | `true`     | Gets or sets whether the checkbox is checked                     |
| **CheckState**                      | `CheckStates`             | `Checked`  | Gets or sets the check state (Checked, Unchecked, Indeterminate) |
| **ThreeState**                      | `bool`                    | `false`    | Enables three-state mode (Checked, Unchecked, Indeterminate)     |
| **Style**                           | `CheckBoxStyles`          | `Tailwind` | Visual style: Tailwind, Flat, or Round                           |
| **ColorScheme**                     | `KtColor`                 | `PRIMARY`  | Color scheme for the checkbox                                    |
| **Label**                           | `Label`                   | `null`     | Label control to bind with the checkbox                          |
| **LabelPosition**                   | `BindingControlPositions` | `Right`    | Position of bound label (Left or Right)                          |
| **AutoCheck**                       | `bool`                    | `true`     | Automatically toggles state on click                             |
| **AnimateCheckBox**                 | `bool`                    | `false`    | Enables checkbox animation on state change                       |
| **AnimateCheckMark**                | `bool`                    | `true`     | Enables checkmark animation on state change                      |
| **BorderRadius**                    | `int`                     | `12`       | Corner radius of the checkbox (1-20)                             |
| **ToolTip**                         | `string`                  | `""`       | Tooltip text displayed on hover                                  |
| **AllowBindingControlLocation**     | `bool`                    | `true`     | Auto-positions bound label relative to checkbox                  |
| **AllowBindingControlColorChanges** | `bool`                    | `true`     | Colorizes bound label on hover                                   |
| **AllowOnHoverStates**              | `bool`                    | `true`     | Enables hover state styling                                      |

***

### State Properties

Each checkbox has multiple state objects that define its appearance:

| State                | Description                           |
| -------------------- | ------------------------------------- |
| **OnCheck**          | Appearance when checked               |
| **OnUncheck**        | Appearance when unchecked             |
| **OnHoverChecked**   | Appearance when hovered and checked   |
| **OnHoverUnchecked** | Appearance when hovered and unchecked |
| **OnDisable**        | Appearance when disabled              |

#### State Properties

Each state object has these properties:

| Property             | Type      | Description              |
| -------------------- | --------- | ------------------------ |
| `CheckBoxColor`      | `KtColor` | Inner fill color         |
| `BorderColor`        | `KtColor` | Border color             |
| `CheckmarkColor`     | `KtColor` | Checkmark color          |
| `BorderRadius`       | `int`     | Corner radius (1-20)     |
| `BorderThickness`    | `int`     | Border thickness         |
| `CheckmarkThickness` | `int`     | Checkmark line thickness |

***

### Events

| Event                             | Arguments                         | Description                              |
| --------------------------------- | --------------------------------- | ---------------------------------------- |
| **CheckedChanged**                | `CheckedChangedEventArgs`         | Fires when Checked property changes      |
| **CheckStateChanged**             | `CheckedChangedEventArgs`         | Fires when CheckState changes            |
| **StatePropertiesChanged**        | `StatePropertiesChangedEventArgs` | Fires when state properties are modified |
| **StylePropertyChanged**          | `StylePropertyChangedEventArgs`   | Fires when Style property changes        |
| **BindingControlChanged**         | `BindingControlChangedEventArgs`  | Fires when bound label changes           |
| **BindingControlPositionChanged** | `PositionChangedEventArgs`        | Fires when label position changes        |

***

### Basic Usage

#### Simple Checkbox

```csharp
var checkbox = new KtCheckBox
{
    Checked = true,
    Location = new Point(20, 20),
    Size = new Size(21, 21)
};

// Handle state changes
checkbox.CheckedChanged += (s, e) =>
{
    bool isChecked = e.Checked;
    MessageBox.Show($"Checkbox is {(isChecked ? "checked" : "unchecked")}");
};

this.Controls.Add(checkbox);
```

#### Checkbox with Label

```csharp
var label = new Label
{
    Text = "Accept Terms and Conditions",
    AutoSize = true
};

var checkbox = new KtCheckBox(false, label)
{
    Location = new Point(20, 50),
    LabelPosition = BindingControlPositions.Right
};

this.Controls.Add(checkbox);
// Label is automatically added and positioned
```

#### Checkbox with Location

```csharp
var label = new Label { Text = "Remember Me", AutoSize = true };

var checkbox = new KtCheckBox(
    isChecked: true,
    label: label,
    location: new Point(30, 100)
);

this.Controls.Add(checkbox);
```

***

### Styling Examples

#### Custom Color Scheme

```csharp
var checkbox = new KtCheckBox
{
    ColorScheme = KtColor.SUCCESS,
    Size = new Size(24, 24)
};
```

#### Round Style

```csharp
var roundCheckbox = new KtCheckBox
{
    Style = KtCheckBox.CheckBoxStyles.Round,
    ColorScheme = KtColor.INFO,
    Size = new Size(26, 26)
};
```

#### Custom Border Radius

```csharp
var customCheckbox = new KtCheckBox
{
    Style = KtCheckBox.CheckBoxStyles.Tailwind,
    BorderRadius = 6,  // Less rounded
    Size = new Size(22, 22)
};
```

#### Flat Style

```csharp
var flatCheckbox = new KtCheckBox
{
    Style = KtCheckBox.CheckBoxStyles.Flat,
    ColorScheme = KtColor.WARNING,
    BorderRadius = 4
};
```

***

### Advanced Features

#### Three-State Checkbox

```csharp
var threeStateCheckbox = new KtCheckBox
{
    ThreeState = true,
    CheckState = KtCheckBox.CheckStates.Indeterminate
};

threeStateCheckbox.CheckStateChanged += (s, e) =>
{
    switch (e.CheckState)
    {
        case KtCheckBox.CheckStates.Checked:
            Console.WriteLine("All items selected");
            break;
        case KtCheckBox.CheckStates.Unchecked:
            Console.WriteLine("No items selected");
            break;
        case KtCheckBox.CheckStates.Indeterminate:
            Console.WriteLine("Some items selected");
            break;
    }
};
```

#### Custom State Styling

```csharp
var checkbox = new KtCheckBox();

// Customize checked state
checkbox.OnCheck.CheckBoxColor = KtColor.PRIMARY;
checkbox.OnCheck.BorderColor = KtColor.PRIMARY;
checkbox.OnCheck.CheckmarkColor = KtColor.WHITE;

// Customize unchecked state
checkbox.OnUncheck.BorderColor = KtColor.BASE_300;

// Customize hover states
checkbox.OnHoverChecked.BorderColor = KtColor.PRIMARY % 80;
checkbox.OnHoverUnchecked.BorderColor = KtColor.BASE_400;

checkbox.Render();
```

#### Animations

```csharp
var animatedCheckbox = new KtCheckBox
{
    AnimateCheckBox = true,      // Animates the box itself
    AnimateCheckMark = true,     // Animates the checkmark
    AllowBindingControlAnimation = true  // Animates bound label
};
```

#### Programmatic Label Binding

```csharp
var checkbox = new KtCheckBox();
var label = new Label { Text = "Enable Notifications", AutoSize = true };

// Bind label
checkbox.Label = label;
checkbox.LabelPosition = BindingControlPositions.Right;
checkbox.AllowBindingControlLocation = true;

this.Controls.Add(checkbox);
```

***

### Label Management

#### Creating Labels Programmatically

```csharp
var checkbox = new KtCheckBox();

// Create and bind a new label
var label = checkbox.NewBindingLabel(
    text: "Subscribe to Newsletter",
    font: new Font("Segoe UI", 9F),
    foreColor: Color.Black
);

this.Controls.Add(checkbox);
```

#### Label Positioning

```csharp
var checkbox = new KtCheckBox();
var label = new Label { Text = "Left-aligned Label", AutoSize = true };

checkbox.Label = label;
checkbox.LabelPosition = BindingControlPositions.Left;  // Place label on left
checkbox.AllowBindingControlLocation = true;

this.Controls.Add(checkbox);
```

#### Disabling Label Color Changes

```csharp
var checkbox = new KtCheckBox();
checkbox.AllowBindingControlColorChanges = false;  // Keep label color constant
```

***

### Common Patterns

#### Checkbox List

```csharp
var options = new[] { "Option 1", "Option 2", "Option 3", "Option 4" };
var checkboxes = new List<KtCheckBox>();

int yPos = 20;
foreach (var option in options)
{
    var label = new Label { Text = option, AutoSize = true };
    var checkbox = new KtCheckBox(false, label, new Point(20, yPos));
    
    checkboxes.Add(checkbox);
    this.Controls.Add(checkbox);
    
    yPos += 35;
}

// Check if all are selected
bool allChecked = checkboxes.All(cb => cb.Checked);
```

#### Select All Pattern

```csharp
var selectAllCheckbox = new KtCheckBox
{
    ThreeState = true,
    Label = new Label { Text = "Select All", AutoSize = true, Font = new Font("Segoe UI", 9F, FontStyle.Bold) }
};

var itemCheckboxes = new List<KtCheckBox>();

// When individual checkbox changes
void ItemCheckbox_CheckedChanged(object sender, EventArgs e)
{
    bool allChecked = itemCheckboxes.All(cb => cb.Checked);
    bool noneChecked = itemCheckboxes.All(cb => !cb.Checked);
    
    if (allChecked)
        selectAllCheckbox.CheckState = KtCheckBox.CheckStates.Checked;
    else if (noneChecked)
        selectAllCheckbox.CheckState = KtCheckBox.CheckStates.Unchecked;
    else
        selectAllCheckbox.CheckState = KtCheckBox.CheckStates.Indeterminate;
}

// When select all changes
selectAllCheckbox.CheckedChanged += (s, e) =>
{
    if (selectAllCheckbox.CheckState != KtCheckBox.CheckStates.Indeterminate)
    {
        foreach (var cb in itemCheckboxes)
            cb.Checked = selectAllCheckbox.Checked;
    }
};
```

#### Settings Panel

```csharp
var settings = new Dictionary<string, KtCheckBox>
{
    ["notifications"] = CreateCheckbox("Enable Notifications", true),
    ["autoSave"] = CreateCheckbox("Auto-save changes", true),
    ["darkMode"] = CreateCheckbox("Dark Mode", false),
    ["soundEffects"] = CreateCheckbox("Sound Effects", true)
};

KtCheckBox CreateCheckbox(string text, bool isChecked)
{
    var label = new Label { Text = text, AutoSize = true };
    return new KtCheckBox(isChecked, label)
    {
        ColorScheme = KtColor.PRIMARY,
        AnimateCheckMark = true
    };
}

// Apply settings
void ApplySettings()
{
    bool notifications = settings["notifications"].Checked;
    bool autoSave = settings["autoSave"].Checked;
    // ... apply other settings
}
```

#### Form Validation

```csharp
var termsCheckbox = new KtCheckBox(false)
{
    Label = new Label { Text = "I agree to the terms and conditions" },
    ColorScheme = KtColor.ERROR
};

var submitButton = new Button { Text = "Submit", Enabled = false };

termsCheckbox.CheckedChanged += (s, e) =>
{
    submitButton.Enabled = termsCheckbox.Checked;
    termsCheckbox.ColorScheme = termsCheckbox.Checked ? KtColor.SUCCESS : KtColor.ERROR;
    termsCheckbox.Render();
};
```

***

### Tooltip Usage

```csharp
var checkbox = new KtCheckBox
{
    ToolTip = "Check this box to enable the feature.\nUncheck to disable it."
};
```

***

### Keyboard Support

The checkbox supports keyboard interaction:

```csharp
var checkbox = new KtCheckBox();

// Space key toggles the checkbox automatically
// The control handles KeyDown events internally
```

***

### State Access in Events

```csharp
checkbox.CheckedChanged += (s, e) =>
{
    bool isChecked = e.Checked;
    KtCheckBox.CheckStates state = e.CheckState;
    
    Console.WriteLine($"Checked: {isChecked}, State: {state}");
};

checkbox.StatePropertiesChanged += (s, e) =>
{
    Color boxColor = e.CheckBoxColor;
    Color borderColor = e.BorderColor;
    Color checkmarkColor = e.CheckmarkColor;
    int radius = e.BorderRadius;
    int borderThickness = e.BorderThickness;
    
    Console.WriteLine($"State changed to: {e.CurrentState.Name}");
};
```

***

### Design Tips

1. **Size Consistency**: Standard size is 21x21, but can be customized. Height automatically adjusts to width
2. **Label Spacing**: The control automatically manages spacing between checkbox and label
3. **Color Scheme**: Use consistent color schemes across your application
4. **Animations**: Enable animations for a more polished user experience
5. **Three-State**: Use for parent-child checkbox relationships (e.g., "Select All")
6. **Hover States**: Keep `AllowOnHoverStates` enabled for better user feedback

***

### Performance Optimization

```csharp
// Batch updates
checkbox.SuspendLayout();
checkbox.ColorScheme = KtColor.PRIMARY;
checkbox.BorderRadius = 8;
checkbox.Style = KtCheckBox.CheckBoxStyles.Round;
checkbox.ResumeLayout(true);

// Manual rendering control
checkbox.AutoCheck = false;
checkbox.Click += (s, e) =>
{
    // Custom logic
    checkbox.Checked = ShouldCheck();
    checkbox.Render();
};
```

***

### Accessibility Features

* Automatic cursor change to hand pointer
* Accessible role set to CheckButton for bound labels
* Keyboard navigation support (Space key to toggle)
* Clear visual states for checked/unchecked/hover
* Tooltip support for additional context

***

### Enumerations

#### CheckBoxStyles

```csharp
public enum CheckBoxStyles
{
    Tailwind,    // Modern Tailwind CSS-inspired design
    Flat,        // Flat, minimalist design
    Round        // Fully circular checkbox
}
```

#### CheckStates

```csharp
public enum CheckStates
{
    Checked,         // Checked state
    Unchecked,       // Unchecked state
    Indeterminate    // Indeterminate/mixed state
}
```

#### BindingControlPositions

```csharp
public enum BindingControlPositions
{
    Left,    // Label positioned to the left
    Right    // Label positioned to the right
}
```

***

### Migration Notes

If migrating from standard CheckBox:

```csharp
// Standard CheckBox
var oldCheckbox = new CheckBox 
{ 
    Text = "Option",
    Checked = true 
};

// KtCheckBox equivalent
var label = new Label { Text = "Option", AutoSize = true };
var newCheckbox = new KtCheckBox(true, label)
{
    ColorScheme = KtColor.PRIMARY
};
```
