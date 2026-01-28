---
icon: circle-dot
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

# Radio Box

### Overview

**KtRadioBox** is a stylish radio button control that enables mutually exclusive selections within a group. With intuitive customization options, smooth rendering, and label binding capabilities, it provides a modern alternative to standard radio buttons for Windows Forms applications.

***

### Key Properties

| Property                        | Type                      | Default   | Description                                               |
| ------------------------------- | ------------------------- | --------- | --------------------------------------------------------- |
| **Checked**                     | `bool`                    | `false`   | Gets or sets whether the radio button is selected         |
| **RadioColor**                  | `KtColor`                 | `PRIMARY` | Inner fill color when checked                             |
| **OutlineColor**                | `KtColor`                 | `PRIMARY` | Outline color when checked                                |
| **OutlineColorUnchecked**       | `KtColor`                 | `PRIMARY` | Outline color when unchecked                              |
| **RadioColorTabFocused**        | `KtColor`                 | `PRIMARY` | Inner fill color when focused                             |
| **OutlineColorTabFocused**      | `KtColor`                 | `PRIMARY` | Outline color when focused                                |
| **BorderThickness**             | `int`                     | `2`       | Thickness of the outline border                           |
| **BindingControl**              | `Control`                 | `null`    | Control to bind with the radio button (typically a Label) |
| **BindingControlPosition**      | `BindingControlPositions` | `Right`   | Position of bound control (Left or Right)                 |
| **AllowBindingControlLocation** | `bool`                    | `false`   | Auto-positions bound control relative to radio button     |

***

### Events

| Event                             | Arguments                        | Description                                   |
| --------------------------------- | -------------------------------- | --------------------------------------------- |
| **CheckedChanged**                | `EventArgs`                      | Fires when the Checked property changes       |
| **CheckedChanged2**               | `CheckedChangedEventArgs`        | Extended event with checked state information |
| **BindingControlChanged**         | `BindingControlChangedEventArgs` | Fires when bound control changes              |
| **BindingControlPositionChanged** | `PositionChangedEventArgs`       | Fires when bound control position changes     |

***

### Basic Usage

#### Simple Radio Button

```csharp
var radioButton = new KtRadioBox
{
    Checked = false,
    Location = new Point(20, 20),
    Size = new Size(21, 21)
};

// Handle state changes
radioButton.CheckedChanged2 += (s, e) =>
{
    bool isChecked = e.Checked;
    MessageBox.Show($"Radio button is {(isChecked ? "selected" : "deselected")}");
};

this.Controls.Add(radioButton);
```

#### Radio Button with Label

```csharp
var label = new Label
{
    Text = "Option 1",
    AutoSize = true,
    Location = new Point(50, 20)
};

var radioButton = new KtRadioBox
{
    Location = new Point(20, 20),
    BindingControl = label,
    BindingControlPosition = KtRadioBox.BindingControlPositions.Right,
    AllowBindingControlLocation = true
};

this.Controls.Add(label);
this.Controls.Add(radioButton);
```

***

### Styling Examples

#### Custom Colors

```csharp
var radioButton = new KtRadioBox
{
    RadioColor = KtColor.SUCCESS,
    OutlineColor = KtColor.SUCCESS,
    OutlineColorUnchecked = KtColor.BASE_300,
    Size = new Size(24, 24)
};
```

#### Custom Border Thickness

```csharp
var thickRadio = new KtRadioBox
{
    BorderThickness = 3,
    RadioColor = KtColor.PRIMARY,
    OutlineColor = KtColor.PRIMARY,
    Size = new Size(26, 26)
};
```

#### Focus States

```csharp
var focusableRadio = new KtRadioBox
{
    RadioColor = KtColor.PRIMARY,
    RadioColorTabFocused = KtColor.SECONDARY,
    OutlineColorTabFocused = KtColor.SECONDARY,
    OutlineColorUnchecked = KtColor.BASE_300
};
```

***

### Radio Button Groups

#### Creating Mutually Exclusive Groups

Radio buttons automatically work together when placed in the same container:

```csharp
// Radio buttons in the same parent automatically form a group
var options = new[]
{
    "Small",
    "Medium", 
    "Large",
    "Extra Large"
};

int yPos = 20;
foreach (var option in options)
{
    var label = new Label
    {
        Text = option,
        AutoSize = true,
        Location = new Point(50, yPos)
    };
    
    var radio = new KtRadioBox
    {
        Location = new Point(20, yPos),
        BindingControl = label,
        AllowBindingControlLocation = true,
        Checked = option == "Medium" // Default selection
    };
    
    this.Controls.Add(label);
    this.Controls.Add(radio);
    
    yPos += 35;
}
```

#### Separate Groups with Panels

```csharp
// Group 1: Size selection
var sizePanel = new Panel
{
    Location = new Point(20, 20),
    Size = new Size(200, 150)
};

var sizeOptions = new[] { "Small", "Medium", "Large" };
int yPos = 10;

foreach (var size in sizeOptions)
{
    var radio = new KtRadioBox
    {
        Location = new Point(10, yPos),
        RadioColor = KtColor.PRIMARY,
        Checked = size == "Medium"
    };
    
    var label = new Label
    {
        Text = size,
        AutoSize = true,
        Location = new Point(40, yPos)
    };
    
    sizePanel.Controls.Add(radio);
    sizePanel.Controls.Add(label);
    
    yPos += 30;
}

// Group 2: Color selection (independent group)
var colorPanel = new Panel
{
    Location = new Point(240, 20),
    Size = new Size(200, 150)
};

var colorOptions = new[] { "Red", "Blue", "Green" };
yPos = 10;

foreach (var color in colorOptions)
{
    var radio = new KtRadioBox
    {
        Location = new Point(10, yPos),
        RadioColor = KtColor.SECONDARY,
        Checked = color == "Blue"
    };
    
    var label = new Label
    {
        Text = color,
        AutoSize = true,
        Location = new Point(40, yPos)
    };
    
    colorPanel.Controls.Add(radio);
    colorPanel.Controls.Add(label);
    
    yPos += 30;
}

this.Controls.Add(sizePanel);
this.Controls.Add(colorPanel);
```

***

### Common Patterns

#### Settings Selection

```csharp
public class SettingsForm : Form
{
    private KtRadioBox radioLight;
    private KtRadioBox radioDark;
    private KtRadioBox radioAuto;
    
    private void InitializeThemeSettings()
    {
        var themes = new Dictionary<string, KtRadioBox>
        {
            ["Light"] = new KtRadioBox { RadioColor = KtColor.WARNING },
            ["Dark"] = new KtRadioBox { RadioColor = KtColor.BASE_300 },
            ["Auto"] = new KtRadioBox { RadioColor = KtColor.INFO, Checked = true }
        };
        
        int yPos = 20;
        foreach (var theme in themes)
        {
            var label = new Label
            {
                Text = $"{theme.Key} Mode",
                Location = new Point(50, yPos),
                AutoSize = true
            };
            
            theme.Value.Location = new Point(20, yPos);
            theme.Value.CheckedChanged2 += ThemeRadio_CheckedChanged;
            
            this.Controls.Add(theme.Value);
            this.Controls.Add(label);
            
            yPos += 35;
        }
    }
    
    private void ThemeRadio_CheckedChanged(object sender, CheckedChangedEventArgs e)
    {
        if (e.Checked)
        {
            var radio = (KtRadioBox)sender;
            // Find which radio was selected and apply theme
            ApplyTheme(radio);
        }
    }
    
    private void ApplyTheme(KtRadioBox selectedRadio)
    {
        // Apply theme logic here
    }
}
```

#### Survey/Questionnaire Pattern

```csharp
public class SurveyQuestion
{
    public string Question { get; set; }
    public List<string> Options { get; set; }
    public KtRadioBox SelectedRadio { get; set; }
}

private List<SurveyQuestion> CreateSurvey()
{
    var questions = new List<SurveyQuestion>
    {
        new SurveyQuestion
        {
            Question = "How satisfied are you with our service?",
            Options = new List<string> 
            { 
                "Very Satisfied", 
                "Satisfied", 
                "Neutral", 
                "Dissatisfied", 
                "Very Dissatisfied" 
            }
        },
        new SurveyQuestion
        {
            Question = "Would you recommend us to others?",
            Options = new List<string> { "Yes", "No", "Maybe" }
        }
    };
    
    int yPos = 20;
    foreach (var question in questions)
    {
        // Question label
        var questionLabel = new Label
        {
            Text = question.Question,
            Location = new Point(20, yPos),
            AutoSize = true,
            Font = new Font("Segoe UI", 10F, FontStyle.Bold)
        };
        this.Controls.Add(questionLabel);
        yPos += 30;
        
        // Create panel for this question's options
        var optionsPanel = new Panel
        {
            Location = new Point(20, yPos),
            Size = new Size(400, question.Options.Count * 35)
        };
        
        int optionY = 0;
        foreach (var option in question.Options)
        {
            var radio = new KtRadioBox
            {
                Location = new Point(20, optionY),
                RadioColor = KtColor.PRIMARY
            };
            
            var label = new Label
            {
                Text = option,
                Location = new Point(50, optionY),
                AutoSize = true
            };
            
            radio.CheckedChanged2 += (s, e) =>
            {
                if (e.Checked) question.SelectedRadio = (KtRadioBox)s;
            };
            
            optionsPanel.Controls.Add(radio);
            optionsPanel.Controls.Add(label);
            
            optionY += 35;
        }
        
        this.Controls.Add(optionsPanel);
        yPos += optionsPanel.Height + 40;
    }
    
    return questions;
}
```

#### Payment Method Selection

```csharp
private void CreatePaymentOptions()
{
    var paymentMethods = new Dictionary<string, (KtColor Color, string Description)>
    {
        ["Credit Card"] = (KtColor.PRIMARY, "Visa, Mastercard, Amex"),
        ["PayPal"] = (KtColor.INFO, "Fast and secure"),
        ["Bank Transfer"] = (KtColor.SUCCESS, "Direct bank payment"),
        ["Cash on Delivery"] = (KtColor.WARNING, "Pay when you receive")
    };
    
    int yPos = 20;
    foreach (var method in paymentMethods)
    {
        var radio = new KtRadioBox
        {
            Location = new Point(20, yPos),
            RadioColor = method.Value.Color,
            OutlineColor = method.Value.Color,
            Size = new Size(24, 24)
        };
        
        var titleLabel = new Label
        {
            Text = method.Key,
            Location = new Point(55, yPos),
            AutoSize = true,
            Font = new Font("Segoe UI", 10F, FontStyle.Bold)
        };
        
        var descLabel = new Label
        {
            Text = method.Value.Description,
            Location = new Point(55, yPos + 20),
            AutoSize = true,
            ForeColor = Color.Gray,
            Font = new Font("Segoe UI", 8F)
        };
        
        radio.CheckedChanged2 += (s, e) =>
        {
            if (e.Checked)
            {
                ProcessPaymentMethod(method.Key);
            }
        };
        
        this.Controls.Add(radio);
        this.Controls.Add(titleLabel);
        this.Controls.Add(descLabel);
        
        yPos += 60;
    }
}
```

#### Getting Selected Value

```csharp
public string GetSelectedOption(Panel container)
{
    foreach (Control control in container.Controls)
    {
        if (control is KtRadioBox radio && radio.Checked)
        {
            // Find associated label or use Tag property
            var label = container.Controls
                .OfType<Label>()
                .FirstOrDefault(l => Math.Abs(l.Location.Y - radio.Location.Y) < 5);
            
            return label?.Text ?? "Unknown";
        }
    }
    
    return null;
}

// Usage
string selectedSize = GetSelectedOption(sizePanel);
if (selectedSize != null)
{
    MessageBox.Show($"You selected: {selectedSize}");
}
```

#### Using Tag Property for Value Storage

```csharp
var options = new[]
{
    new { Display = "Basic Plan - $9.99/mo", Value = "BASIC" },
    new { Display = "Pro Plan - $19.99/mo", Value = "PRO" },
    new { Display = "Enterprise Plan - $49.99/mo", Value = "ENTERPRISE" }
};

foreach (var option in options)
{
    var radio = new KtRadioBox
    {
        Tag = option.Value,  // Store the value
        RadioColor = KtColor.PRIMARY
    };
    
    var label = new Label
    {
        Text = option.Display,
        AutoSize = true
    };
    
    radio.BindingControl = label;
    radio.AllowBindingControlLocation = true;
    
    radio.CheckedChanged2 += (s, e) =>
    {
        if (e.Checked)
        {
            string planValue = ((KtRadioBox)s).Tag.ToString();
            ProcessPlanSelection(planValue);
        }
    };
    
    this.Controls.Add(radio);
}
```

***

### Advanced Features

#### Programmatic Selection

```csharp
// Select a specific radio button
radioButton1.Checked = true;  // Automatically unchecks others in the group

// Find and select by criteria
foreach (Control control in panel.Controls)
{
    if (control is KtRadioBox radio && radio.Tag?.ToString() == "PREMIUM")
    {
        radio.Checked = true;
        break;
    }
}
```

#### Keyboard Navigation

```csharp
// The control automatically supports keyboard navigation
// Space or Enter keys toggle selection

radioButton.KeyDown += (s, e) =>
{
    if (e.KeyCode == Keys.Space || e.KeyCode == Keys.Enter)
    {
        // Custom logic on keyboard selection
        Console.WriteLine("Selected via keyboard");
    }
};
```

#### Focus Management

```csharp
var radioButton = new KtRadioBox
{
    RadioColorTabFocused = KtColor.ACCENT,
    OutlineColorTabFocused = KtColor.ACCENT
};

radioButton.GotFocus += (s, e) =>
{
    // Handle focus gained
    Console.WriteLine("Radio button focused");
};

radioButton.LostFocus += (s, e) =>
{
    // Handle focus lost
    Console.WriteLine("Radio button lost focus");
};

// Programmatically set focus
radioButton.Focus();
```

#### Dynamic Group Creation

```csharp
private Panel CreateRadioGroup(string title, string[] options, string defaultSelection = null)
{
    var panel = new Panel
    {
        Size = new Size(250, 40 + (options.Length * 35)),
        BorderStyle = BorderStyle.FixedSingle
    };
    
    var titleLabel = new Label
    {
        Text = title,
        Location = new Point(10, 10),
        Font = new Font("Segoe UI", 10F, FontStyle.Bold),
        AutoSize = true
    };
    panel.Controls.Add(titleLabel);
    
    int yPos = 40;
    foreach (var option in options)
    {
        var radio = new KtRadioBox
        {
            Location = new Point(20, yPos),
            RadioColor = KtColor.PRIMARY,
            Checked = option == defaultSelection
        };
        
        var label = new Label
        {
            Text = option,
            Location = new Point(50, yPos),
            AutoSize = true
        };
        
        label.Click += (s, e) => radio.Checked = true;
        
        panel.Controls.Add(radio);
        panel.Controls.Add(label);
        
        yPos += 35;
    }
    
    return panel;
}

// Usage
var shippingPanel = CreateRadioGroup(
    "Shipping Method",
    new[] { "Standard (5-7 days)", "Express (2-3 days)", "Overnight" },
    "Standard (5-7 days)"
);
this.Controls.Add(shippingPanel);
```

***

### Label Binding Features

#### Automatic Label Positioning

```csharp
var label = new Label
{
    Text = "Enable Feature",
    AutoSize = true
};

var radio = new KtRadioBox
{
    Location = new Point(20, 50),
    BindingControl = label,
    BindingControlPosition = KtRadioBox.BindingControlPositions.Right,
    AllowBindingControlLocation = true  // Automatically positions label
};

this.Controls.Add(radio);
// Label position is managed automatically
```

#### Left-Aligned Labels

```csharp
var radio = new KtRadioBox
{
    Location = new Point(200, 50),
    BindingControl = new Label { Text = "Left Label", AutoSize = true },
    BindingControlPosition = KtRadioBox.BindingControlPositions.Left,
    AllowBindingControlLocation = true
};
```

#### Manual Label Positioning

```csharp
var radio = new KtRadioBox
{
    Location = new Point(20, 50),
    AllowBindingControlLocation = false  // Disable automatic positioning
};

var label = new Label
{
    Text = "Custom Position",
    Location = new Point(50, 52),  // Manually positioned
    AutoSize = true
};

radio.BindingControl = label;

this.Controls.Add(radio);
this.Controls.Add(label);
```

***

### Validation and Error Handling

```csharp
private bool ValidateRadioSelection(Panel container, string fieldName)
{
    bool hasSelection = container.Controls
        .OfType<KtRadioBox>()
        .Any(r => r.Checked);
    
    if (!hasSelection)
    {
        MessageBox.Show(
            $"Please select a {fieldName}",
            "Validation Error",
            MessageBoxButtons.OK,
            MessageBoxIcon.Warning
        );
        return false;
    }
    
    return true;
}

// Usage
private void SubmitButton_Click(object sender, EventArgs e)
{
    if (!ValidateRadioSelection(sizePanel, "size"))
        return;
    
    if (!ValidateRadioSelection(colorPanel, "color"))
        return;
    
    // Proceed with form submission
    ProcessForm();
}
```

***

### Design Tips

1. **Consistent Sizing**: Keep radio buttons at 21x21 or scale proportionally (Height automatically matches Width)
2. **Group Organization**: Use panels to create distinct radio button groups
3. **Color Coding**: Use different colors for different types of selections
4. **Clear Labels**: Always provide descriptive labels for each option
5. **Default Selection**: Consider pre-selecting the most common option
6. **Focus States**: Customize focus colors for better keyboard navigation feedback
7. **Spacing**: Maintain consistent vertical spacing (30-35px) between options

***

### Accessibility Features

* Automatic mutual exclusion within the same container
* Keyboard navigation support (Space/Enter keys)
* Focus state visualization
* Accessible role support for bound controls
* Cursor change to hand pointer on hover
* Clear visual distinction between checked/unchecked states

***

### Performance Notes

* Radio buttons automatically manage sibling selections
* Only one radio button can be checked per parent container
* Use `Tag` property to store associated values
* Group related radio buttons in panels for better organization

***

### Enumerations

#### BindingControlPositions

```csharp
public enum BindingControlPositions
{
    Left,    // Positions bound control to the left
    Right    // Positions bound control to the right
}
```

***

### Migration Notes

If migrating from standard RadioButton:

```csharp
// Standard RadioButton
var oldRadio = new RadioButton
{
    Text = "Option 1",
    Location = new Point(20, 20),
    Checked = true
};

// KtRadioBox equivalent
var label = new Label { Text = "Option 1", AutoSize = true };
var newRadio = new KtRadioBox
{
    Location = new Point(20, 20),
    BindingControl = label,
    AllowBindingControlLocation = true,
    Checked = true,
    RadioColor = KtColor.PRIMARY
};
```
