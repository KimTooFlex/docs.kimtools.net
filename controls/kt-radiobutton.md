---
layout:
  width: wide
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

# 🔹 Kt-RadioButton

### Overview

**KtRadioButton** is a modern radio button control rendered as a styled button that provides mutually exclusive selections with rich visual customization. Combining the functionality of traditional radio buttons with the appearance of buttons, it offers gradient backgrounds, icons, and smooth state transitions for creating engaging user interfaces in Windows Forms applications.

***

### Key Properties

| Property                 | Type               | Default                              | Description                                       |
| ------------------------ | ------------------ | ------------------------------------ | ------------------------------------------------- |
| **Checked**              | `bool`             | `false`                              | Gets or sets whether the radio button is selected |
| **Text**                 | `string`           | `""`                                 | The text displayed on the button                  |
| **Icon**                 | `string`           | `""`                                 | Icon identifier for unchecked state               |
| **Icon\_Checked**        | `string`           | `"tabler.solid.circle_check_filled"` | Icon identifier for checked state                 |
| **Background**           | `KtBrush`          | `Solid`                              | Background brush for unchecked state              |
| **Background\_Checked**  | `KtBrush`          | `Solid`                              | Background brush for checked state                |
| **Border**               | `KtBrush`          | `Gradient`                           | Border brush for unchecked state                  |
| **Border\_Checked**      | `KtBrush`          | `Solid`                              | Border brush for checked state                    |
| **BorderRadius**         | `float`            | `10`                                 | Roundness of button corners                       |
| **BorderWidth**          | `float`            | `2`                                  | Thickness of the border                           |
| **BorderStyle**          | `DashStyle`        | `Solid`                              | Border style for unchecked state                  |
| **BorderStyle\_Checked** | `DashStyle`        | `Solid`                              | Border style for checked state                    |
| **Foreground**           | `KtColor`          | `Empty`                              | Text/icon color for unchecked state               |
| **Foreground\_Checked**  | `KtColor`          | `Empty`                              | Text/icon color for checked state                 |
| **IconColor**            | `KtColor`          | `Empty`                              | Icon color for unchecked state                    |
| **IconColor\_Checked**   | `KtColor`          | `Empty`                              | Icon color for checked state                      |
| **IconSize**             | `int`              | `16`                                 | Size of the icon in pixels                        |
| **IconStroke**           | `double`           | `2.5`                                | Stroke width for icon rendering                   |
| **TextAlign**            | `ContentAlignment` | `MiddleCenter`                       | Alignment of text within button                   |
| **ImageAlign**           | `ContentAlignment` | `MiddleLeft`                         | Alignment of icon within button                   |
| **TextMargin**           | `int`              | `0`                                  | Spacing between text and icon                     |
| **Padding**              | `Padding`          | `7,7,7,7`                            | Internal padding of button content                |

***

### Events

| Event              | Description                               |
| ------------------ | ----------------------------------------- |
| **CheckedChanged** | Fires when the `Checked` property changes |

***

### Basic Usage

#### Simple Radio Button

```csharp
var radioButton = new KtRadioButton
{
    Text = "Option 1",
    Location = new Point(20, 20),
    Size = new Size(150, 40)
};

// Handle state changes
radioButton.CheckedChanged += (s, e) =>
{
    var isChecked = ((KtRadioButton)s).Checked;
    MessageBox.Show($"Option 1 is now {(isChecked ? "selected" : "deselected")}");
};

this.Controls.Add(radioButton);
```

#### Radio Button with Icon

```csharp
var iconRadio = new KtRadioButton
{
    Text = "Premium Plan",
    Icon = "tabler.circle",
    Icon_Checked = "tabler.circle_check_filled",
    IconSize = 20,
    TextAlign = ContentAlignment.MiddleCenter,
    ImageAlign = ContentAlignment.MiddleLeft,
    Size = new Size(160, 45)
};
```

***

### Styling Examples

#### Gradient Background

```csharp
var gradientRadio = new KtRadioButton
{
    Text = "Option A",
    Background = KtBrush.Solid,
    Background_Checked = new KtBrushGradient
    {
        StartColor = KtColor.PRIMARY,
        StopColor = KtColor.SECONDARY,
        Angle = 45
    },
    BorderRadius = 15,
    Foreground_Checked = KtColor.WHITE,
    Size = new Size(140, 40)
};
```

#### Solid Color Style

```csharp
var solidRadio = new KtRadioButton
{
    Text = "Standard",
    Background = new KtBrushSolid { Color = KtColor.BASE_1 },
    Background_Checked = new KtBrushSolid { Color = KtColor.PRIMARY },
    Border = new KtBrushSolid { Color = KtColor.BASE_300 },
    Border_Checked = new KtBrushSolid { Color = KtColor.PRIMARY },
    Foreground_Checked = KtColor.WHITE,
    BorderRadius = 10,
    Size = new Size(120, 40)
};
```

#### Outline Style

```csharp
var outlineRadio = new KtRadioButton
{
    Text = "Outline",
    Background = KtBrush.None,
    Background_Checked = KtBrush.None,
    Border = new KtBrushSolid { Color = KtColor.PRIMARY },
    Border_Checked = new KtBrushSolid { Color = KtColor.PRIMARY },
    BorderWidth = 2,
    Foreground = KtColor.PRIMARY,
    Foreground_Checked = KtColor.PRIMARY,
    Size = new Size(120, 40)
};
```

#### Rounded Pill Style

```csharp
var pillRadio = new KtRadioButton
{
    Text = "Pill Style",
    BorderRadius = 25,
    Background_Checked = new KtBrushSolid { Color = KtColor.SUCCESS },
    Foreground_Checked = KtColor.WHITE,
    Size = new Size(140, 50)
};
```

***

### Radio Button Groups

#### Creating Mutually Exclusive Groups

Radio buttons in the same container automatically form a mutually exclusive group:

```csharp
// Create a button group for size selection
var sizeOptions = new[] { "Small", "Medium", "Large", "X-Large" };
var sizeButtons = new List<KtRadioButton>();

int xPos = 20;
foreach (var size in sizeOptions)
{
    var radio = new KtRadioButton
    {
        Text = size,
        Location = new Point(xPos, 20),
        Size = new Size(100, 40),
        Background_Checked = new KtBrushSolid { Color = KtColor.PRIMARY },
        Foreground_Checked = KtColor.WHITE,
        Checked = size == "Medium" // Default selection
    };
    
    sizeButtons.Add(radio);
    this.Controls.Add(radio);
    
    xPos += 110;
}
```

#### Separate Groups with Panels

```csharp
// Panel 1: Shipping Method
var shippingPanel = new Panel
{
    Location = new Point(20, 20),
    Size = new Size(400, 60),
    BorderStyle = BorderStyle.FixedSingle
};

var shippingOptions = new[] { "Standard", "Express", "Overnight" };
int xPos = 10;

foreach (var option in shippingOptions)
{
    var radio = new KtRadioButton
    {
        Text = option,
        Location = new Point(xPos, 10),
        Size = new Size(120, 40),
        Background_Checked = new KtBrushSolid { Color = KtColor.INFO },
        Foreground_Checked = KtColor.WHITE,
        Checked = option == "Standard"
    };
    
    shippingPanel.Controls.Add(radio);
    xPos += 130;
}

// Panel 2: Payment Method (independent group)
var paymentPanel = new Panel
{
    Location = new Point(20, 100),
    Size = new Size(400, 60),
    BorderStyle = BorderStyle.FixedSingle
};

var paymentOptions = new[] { "Credit Card", "PayPal", "Bank Transfer" };
xPos = 10;

foreach (var option in paymentOptions)
{
    var radio = new KtRadioButton
    {
        Text = option,
        Location = new Point(xPos, 10),
        Size = new Size(120, 40),
        Background_Checked = new KtBrushSolid { Color = KtColor.SUCCESS },
        Foreground_Checked = KtColor.WHITE,
        Checked = option == "Credit Card"
    };
    
    paymentPanel.Controls.Add(radio);
    xPos += 130;
}

this.Controls.Add(shippingPanel);
this.Controls.Add(paymentPanel);
```

***

### Common Patterns

#### Horizontal Button Group

```csharp
private void CreateHorizontalButtonGroup()
{
    var options = new Dictionary<string, KtColor>
    {
        ["Daily"] = KtColor.PRIMARY,
        ["Weekly"] = KtColor.SECONDARY,
        ["Monthly"] = KtColor.INFO,
        ["Yearly"] = KtColor.SUCCESS
    };
    
    int xPos = 20;
    foreach (var option in options)
    {
        var radio = new KtRadioButton
        {
            Text = option.Key,
            Location = new Point(xPos, 20),
            Size = new Size(100, 45),
            Background = new KtBrushSolid { Color = KtColor.BASE_1 },
            Background_Checked = new KtBrushSolid { Color = option.Value },
            Border = new KtBrushSolid { Color = option.Value },
            Foreground = option.Value,
            Foreground_Checked = KtColor.WHITE,
            BorderRadius = 8,
            Checked = option.Key == "Monthly"
        };
        
        radio.CheckedChanged += (s, e) =>
        {
            if (((KtRadioButton)s).Checked)
            {
                UpdateDataView(((KtRadioButton)s).Text);
            }
        };
        
        this.Controls.Add(radio);
        xPos += 110;
    }
}
```

#### Vertical Stack with Icons

```csharp
private void CreateVerticalIconStack()
{
    var plans = new[]
    {
        new { Name = "Basic", Icon = "tabler.user", Price = "$9.99/mo", Color = KtColor.BASE_300 },
        new { Name = "Pro", Icon = "tabler.star", Price = "$19.99/mo", Color = KtColor.PRIMARY },
        new { Name = "Enterprise", Icon = "tabler.building", Price = "$49.99/mo", Color = KtColor.SUCCESS }
    };
    
    int yPos = 20;
    foreach (var plan in plans)
    {
        var radio = new KtRadioButton
        {
            Text = $"{plan.Name}\n{plan.Price}",
            Icon = plan.Icon,
            Icon_Checked = plan.Icon,
            IconSize = 24,
            Location = new Point(20, yPos),
            Size = new Size(200, 60),
            TextAlign = ContentAlignment.MiddleCenter,
            ImageAlign = ContentAlignment.MiddleLeft,
            Background_Checked = new KtBrushSolid { Color = plan.Color },
            Foreground_Checked = KtColor.WHITE,
            IconColor = plan.Color,
            IconColor_Checked = KtColor.WHITE,
            BorderRadius = 12,
            Padding = new Padding(15, 10, 15, 10)
        };
        
        this.Controls.Add(radio);
        yPos += 70;
    }
}
```

#### Card-Style Selection

```csharp
private void CreateCardStyleOptions()
{
    var subscriptions = new[]
    {
        new { Title = "Monthly", Price = "$12", Icon = "tabler.calendar_month" },
        new { Title = "Quarterly", Price = "$32", Badge = "Save 10%", Icon = "tabler.calendar" },
        new { Title = "Annual", Price = "$99", Badge = "Save 30%", Icon = "tabler.calendar_year" }
    };
    
    int xPos = 20;
    foreach (var sub in subscriptions)
    {
        var radio = new KtRadioButton
        {
            Text = $"{sub.Title}\n{sub.Price}/mo",
            Icon = sub.Icon,
            Icon_Checked = sub.Icon,
            IconSize = 28,
            Location = new Point(xPos, 20),
            Size = new Size(140, 80),
            TextAlign = ContentAlignment.BottomCenter,
            ImageAlign = ContentAlignment.TopCenter,
            Background = new KtBrushSolid { Color = KtColor.BASE_1 },
            Background_Checked = new KtBrushGradient
            {
                StartColor = KtColor.PRIMARY,
                StopColor = KtColor.SECONDARY,
                Angle = 135
            },
            Border = new KtBrushSolid { Color = KtColor.BASE_300 },
            Foreground_Checked = KtColor.WHITE,
            IconColor_Checked = KtColor.WHITE,
            BorderRadius = 15,
            BorderWidth = 2
        };
        
        this.Controls.Add(radio);
        xPos += 150;
    }
}
```

#### Tab-Style Navigation

```csharp
private Panel CreateTabNavigation()
{
    var tabPanel = new Panel
    {
        Location = new Point(0, 0),
        Size = new Size(600, 50),
        BackColor = Color.White
    };
    
    var tabs = new[] { "Overview", "Analytics", "Reports", "Settings" };
    int xPos = 0;
    
    foreach (var tab in tabs)
    {
        var radio = new KtRadioButton
        {
            Text = tab,
            Location = new Point(xPos, 5),
            Size = new Size(150, 40),
            Background = KtBrush.None,
            Background_Checked = KtBrush.None,
            Border = KtBrush.None,
            BorderRadius = 8,
            Foreground = KtColor.BASE_CONTENT,
            Foreground_Checked = KtColor.PRIMARY,
            TextAlign = ContentAlignment.MiddleCenter
        };
        
        // Add bottom border effect for checked state
        radio.CheckedChanged += (s, e) =>
        {
            if (((KtRadioButton)s).Checked)
            {
                LoadTabContent(((KtRadioButton)s).Text);
            }
        };
        
        tabPanel.Controls.Add(radio);
        xPos += 150;
    }
    
    return tabPanel;
}
```

#### Getting Selected Value

```csharp
public string GetSelectedValue(Panel container)
{
    foreach (Control control in container.Controls)
    {
        if (control is KtRadioButton radio && radio.Checked)
        {
            return radio.Text;
        }
    }
    
    return null;
}

// Usage
string selectedShipping = GetSelectedValue(shippingPanel);
if (selectedShipping != null)
{
    MessageBox.Show($"Selected shipping: {selectedShipping}");
}
```

#### Using Tag Property

```csharp
var options = new[]
{
    new { Display = "Personal - Free", Value = "PERSONAL" },
    new { Display = "Professional - $29", Value = "PRO" },
    new { Display = "Business - $99", Value = "BUSINESS" }
};

foreach (var option in options)
{
    var radio = new KtRadioButton
    {
        Text = option.Display,
        Tag = option.Value,  // Store the actual value
        Size = new Size(180, 45),
        Background_Checked = new KtBrushSolid { Color = KtColor.PRIMARY },
        Foreground_Checked = KtColor.WHITE
    };
    
    radio.CheckedChanged += (s, e) =>
    {
        if (((KtRadioButton)s).Checked)
        {
            string value = ((KtRadioButton)s).Tag.ToString();
            ProcessSelection(value);
        }
    };
    
    this.Controls.Add(radio);
}
```

***

### Advanced Features

#### Custom Icon Colors

```csharp
var customIconRadio = new KtRadioButton
{
    Text = "Favorite",
    Icon = "tabler.heart",
    Icon_Checked = "tabler.heart_filled",
    IconColor = KtColor.BASE_300,
    IconColor_Checked = KtColor.ERROR,
    IconSize = 22,
    IconStroke = 2.0,
    Background_Checked = new KtBrushSolid { Color = KtColor.ERROR % 10 },
    Foreground_Checked = KtColor.ERROR
};
```

#### Dynamic Border Styles

```csharp
var dashedRadio = new KtRadioButton
{
    Text = "Dashed Border",
    BorderStyle = DashStyle.Dash,
    BorderStyle_Checked = DashStyle.Solid,
    BorderWidth = 2,
    Border = new KtBrushSolid { Color = KtColor.PRIMARY },
    Border_Checked = new KtBrushSolid { Color = KtColor.PRIMARY },
    Size = new Size(150, 40)
};
```

#### Programmatic Control

```csharp
// Select a radio button
radioButton1.Checked = true;

// Find and select by criteria
foreach (Control control in panel.Controls)
{
    if (control is KtRadioButton radio && radio.Tag?.ToString() == "PREMIUM")
    {
        radio.Checked = true;
        break;
    }
}

// Refresh appearance
radioButton1.Render();

// Batch updates
radioButton1.SuspendLayout();
radioButton1.Background_Checked = new KtBrushSolid { Color = KtColor.SUCCESS };
radioButton1.BorderRadius = 15;
radioButton1.ResumeLayout(true);
```

#### Text and Icon Alignment

```csharp
// Icon on top, text below
var topIconRadio = new KtRadioButton
{
    Text = "Upload",
    Icon = "tabler.upload",
    Icon_Checked = "tabler.upload",
    ImageAlign = ContentAlignment.TopCenter,
    TextAlign = ContentAlignment.BottomCenter,
    IconSize = 32,
    Size = new Size(100, 100),
    Padding = new Padding(10, 15, 10, 10)
};

// Icon on right, text on left
var rightIconRadio = new KtRadioButton
{
    Text = "Next",
    Icon = "tabler.arrow_right",
    Icon_Checked = "tabler.arrow_right",
    ImageAlign = ContentAlignment.MiddleRight,
    TextAlign = ContentAlignment.MiddleLeft,
    TextMargin = 5
};
```

***

### Responsive Layouts

#### Auto-Adjust Based on Container

```csharp
private void CreateResponsiveButtonGroup(FlowLayoutPanel container)
{
    var options = new[] { "Option 1", "Option 2", "Option 3", "Option 4" };
    
    foreach (var option in options)
    {
        var radio = new KtRadioButton
        {
            Text = option,
            Size = new Size(120, 40),
            Margin = new Padding(5),
            Background_Checked = new KtBrushSolid { Color = KtColor.PRIMARY },
            Foreground_Checked = KtColor.WHITE
        };
        
        container.Controls.Add(radio);
    }
    
    container.FlowDirection = FlowDirection.LeftToRight;
    container.WrapContents = true;
    container.AutoScroll = true;
}
```

#### Grid Layout

```csharp
private void CreateGridLayout()
{
    var tableLayout = new TableLayoutPanel
    {
        Location = new Point(20, 20),
        Size = new Size(400, 200),
        ColumnCount = 2,
        RowCount = 3
    };
    
    tableLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 50));
    tableLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 50));
    
    var options = new[] { "Option 1", "Option 2", "Option 3", "Option 4", "Option 5", "Option 6" };
    
    for (int i = 0; i < options.Length; i++)
    {
        var radio = new KtRadioButton
        {
            Text = options[i],
            Dock = DockStyle.Fill,
            Margin = new Padding(5),
            Background_Checked = new KtBrushSolid { Color = KtColor.PRIMARY },
            Foreground_Checked = KtColor.WHITE
        };
        
        tableLayout.Controls.Add(radio, i % 2, i / 2);
    }
    
    this.Controls.Add(tableLayout);
}
```

***

### Validation

```csharp
private bool ValidateRadioSelection(Panel container, string fieldName)
{
    bool hasSelection = container.Controls
        .OfType<KtRadioButton>()
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

// Highlight missing selection
private void HighlightRequiredField(Panel container)
{
    bool hasSelection = container.Controls
        .OfType<KtRadioButton>()
        .Any(r => r.Checked);
    
    if (!hasSelection)
    {
        container.BackColor = Color.FromArgb(255, 240, 240);
        // Reset after selection
        foreach (var radio in container.Controls.OfType<KtRadioButton>())
        {
            radio.CheckedChanged += (s, e) =>
            {
                if (((KtRadioButton)s).Checked)
                    container.BackColor = Color.White;
            };
        }
    }
}
```

***

### Design Tips

1. **Consistent Sizing**: Use uniform sizes within a button group for visual harmony
2. **Color Schemes**: Use checked state colors that clearly indicate selection
3. **Icon Usage**: Choose meaningful icons that represent the option
4. **Spacing**: Maintain 10-15px spacing between buttons in horizontal layouts
5. **Border Radius**: Match border radius with your application's design language
6. **Text Length**: Keep button text concise for better readability
7. **Hover Feedback**: The control automatically provides hover effects
8. **Default Selection**: Pre-select the most common or recommended option

***

### Performance Optimization

```csharp
// Batch updates for multiple properties
radio.SuspendLayout();
radio.Background_Checked = newBrush;
radio.BorderRadius = 12;
radio.Foreground_Checked = newColor;
radio.ResumeLayout(true);

// Efficient group creation
var buttons = Enumerable.Range(1, 10)
    .Select(i => new KtRadioButton
    {
        Text = $"Option {i}",
        Size = new Size(100, 40),
        Tag = i
    })
    .ToArray();

foreach (var btn in buttons)
    this.Controls.Add(btn);
```

***

### Accessibility Features

* Automatic cursor change to hand pointer
* Keyboard navigation support (Space/Enter keys)
* Clear visual states for checked/unchecked
* Focus state visualization
* Mutually exclusive selection within groups
* RTL (Right-to-Left) text support

***

### Migration Notes

If migrating from standard RadioButton:

```csharp
// Standard RadioButton
var oldRadio = new RadioButton
{
    Text = "Option 1",
    Location = new Point(20, 20),
    Appearance = Appearance.Button,
    Checked = true
};

// KtRadioButton equivalent
var newRadio = new KtRadioButton
{
    Text = "Option 1",
    Location = new Point(20, 20),
    Size = new Size(120, 40),
    Background_Checked = new KtBrushSolid { Color = KtColor.PRIMARY },
    Foreground_Checked = KtColor.WHITE,
    Checked = true
};
```
