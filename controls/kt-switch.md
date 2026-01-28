---
icon: toggle-large-on
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

# Switch

### Overview

**KtSwitch** is a modern, customizable toggle switch control that provides an intuitive way to switch between on/off states for settings and features. With smooth animations, flexible styling options, and distinct visual states, it offers a sleek alternative to traditional checkboxes for binary choices in Windows Forms applications.

***

### Key Properties

| Property              | Type            | Default   | Description                                           |
| --------------------- | --------------- | --------- | ----------------------------------------------------- |
| **Checked**           | `bool`          | `false`   | Gets or sets whether the switch is in the ON position |
| **Value**             | `bool`          | `false`   | Alternative property for checked state                |
| **Bg**                | `KtColor`       | `PRIMARY` | Background color of the switch track                  |
| **Thumb**             | `KtColor`       | `Empty`   | Color of the sliding thumb/circle                     |
| **StateOn**           | `KtSwitchState` | -         | Visual properties when switch is ON                   |
| **StateOff**          | `KtSwitchState` | -         | Visual properties when switch is OFF                  |
| **Animation**         | `int`           | `5`       | Speed of the sliding animation                        |
| **ThumbMargin**       | `int`           | `5`       | Padding/margin around the thumb circle                |
| **BorderRadius**      | `int?`          | `null`    | Corner radius of the switch track                     |
| **BorderRadiusThumb** | `int?`          | `null`    | Corner radius of the thumb circle                     |
| **BorderThickness**   | `int?`          | `2`       | Thickness of the border                               |

***

### State Properties (KtSwitchState)

Each state object (StateOn/StateOff) has these properties:

| Property   | Type      | Description                          |
| ---------- | --------- | ------------------------------------ |
| **Bg**     | `KtColor` | Background color of the switch track |
| **Thumb**  | `KtColor` | Color of the sliding thumb           |
| **Border** | `KtColor` | Border color of the switch           |

***

### Events

| Event              | Arguments                 | Description                         |
| ------------------ | ------------------------- | ----------------------------------- |
| **CheckedChanged** | `CheckedChangedEventArgs` | Fires when the switch state changes |
| **OnValuechange**  | `EventArgs`               | Alternative event for value changes |

***

### Basic Usage

#### Simple Switch

```csharp
var toggle = new KtSwitch
{
    Location = new Point(20, 20),
    Size = new Size(60, 30),
    Checked = false
};

// Handle state changes
toggle.CheckedChanged += (s, e) =>
{
    bool isOn = e.Checked;
    MessageBox.Show($"Switch is now {(isOn ? "ON" : "OFF")}");
};

this.Controls.Add(toggle);
```

#### Switch with Label

```csharp
var label = new Label
{
    Text = "Enable Notifications",
    Location = new Point(90, 25),
    AutoSize = true
};

var toggle = new KtSwitch
{
    Location = new Point(20, 20),
    Size = new Size(60, 30),
    Checked = true
};

toggle.CheckedChanged += (s, e) =>
{
    label.Text = e.Checked ? "Notifications Enabled" : "Notifications Disabled";
};

this.Controls.Add(toggle);
this.Controls.Add(label);
```

***

### Styling Examples

#### Custom Colors

```csharp
var coloredSwitch = new KtSwitch
{
    Size = new Size(60, 30),
    Bg = KtColor.SUCCESS,
    Thumb = KtColor.WHITE
};
```

#### Using State Properties

```csharp
var styledSwitch = new KtSwitch
{
    Size = new Size(70, 35)
};

// Configure OFF state
styledSwitch.StateOff.Bg = KtColor.BASE_300;
styledSwitch.StateOff.Thumb = KtColor.BASE_CONTENT;
styledSwitch.StateOff.Border = KtColor.BASE_300;

// Configure ON state
styledSwitch.StateOn.Bg = KtColor.PRIMARY;
styledSwitch.StateOn.Thumb = KtColor.WHITE;
styledSwitch.StateOn.Border = KtColor.PRIMARY;
```

#### iOS-Style Switch

```csharp
var iosSwitch = new KtSwitch
{
    Size = new Size(55, 30),
    BorderRadius = 15,
    BorderRadiusThumb = 13,
    ThumbMargin = 3
};

iosSwitch.StateOff.Bg = KtColor.BASE_300;
iosSwitch.StateOff.Thumb = KtColor.WHITE;
iosSwitch.StateOff.Border = KtColor.BASE_300;

iosSwitch.StateOn.Bg = KtColor.SUCCESS;
iosSwitch.StateOn.Thumb = KtColor.WHITE;
iosSwitch.StateOn.Border = KtColor.SUCCESS;
```

#### Material Design Style

```csharp
var materialSwitch = new KtSwitch
{
    Size = new Size(50, 25),
    BorderRadius = 12,
    ThumbMargin = 2,
    Animation = 8
};

materialSwitch.StateOff.Bg = Color.Transparent;
materialSwitch.StateOff.Thumb = KtColor.BASE_400;
materialSwitch.StateOff.Border = KtColor.BASE_400;

materialSwitch.StateOn.Bg = KtColor.PRIMARY % 30;
materialSwitch.StateOn.Thumb = KtColor.PRIMARY;
materialSwitch.StateOn.Border = KtColor.PRIMARY;
```

#### Minimal Flat Style

```csharp
var flatSwitch = new KtSwitch
{
    Size = new Size(60, 28),
    BorderRadius = 5,
    BorderThickness = 1
};

flatSwitch.StateOff.Bg = Color.Transparent;
flatSwitch.StateOff.Thumb = KtColor.BASE_CONTENT;
flatSwitch.StateOff.Border = KtColor.BASE_CONTENT;

flatSwitch.StateOn.Bg = KtColor.PRIMARY;
flatSwitch.StateOn.Thumb = KtColor.WHITE;
flatSwitch.StateOn.Border = KtColor.PRIMARY;
```

***

### Common Patterns

#### Settings Panel

```csharp
private void CreateSettingsPanel()
{
    var settings = new Dictionary<string, (KtSwitch Switch, Label Label)>
    {
        ["notifications"] = CreateSetting("Enable Notifications", true),
        ["autoSave"] = CreateSetting("Auto-save changes", true),
        ["darkMode"] = CreateSetting("Dark Mode", false),
        ["sounds"] = CreateSetting("Sound Effects", true)
    };
    
    int yPos = 20;
    foreach (var setting in settings)
    {
        setting.Value.Label.Location = new Point(20, yPos + 5);
        setting.Value.Switch.Location = new Point(250, yPos);
        
        this.Controls.Add(setting.Value.Label);
        this.Controls.Add(setting.Value.Switch);
        
        yPos += 50;
    }
}

private (KtSwitch Switch, Label Label) CreateSetting(string text, bool isChecked)
{
    var label = new Label
    {
        Text = text,
        AutoSize = true,
        Font = new Font("Segoe UI", 10F)
    };
    
    var toggle = new KtSwitch
    {
        Size = new Size(60, 30),
        Checked = isChecked
    };
    
    toggle.StateOn.Bg = KtColor.PRIMARY;
    toggle.StateOn.Thumb = KtColor.WHITE;
    
    return (toggle, label);
}
```

#### Feature Toggles

```csharp
private void CreateFeatureToggles()
{
    var features = new[]
    {
        new { Name = "Beta Features", Description = "Try experimental features", Color = KtColor.WARNING },
        new { Name = "Analytics", Description = "Help improve our product", Color = KtColor.INFO },
        new { Name = "Auto-Update", Description = "Automatically download updates", Color = KtColor.SUCCESS }
    };
    
    int yPos = 20;
    foreach (var feature in features)
    {
        var titleLabel = new Label
        {
            Text = feature.Name,
            Location = new Point(20, yPos),
            AutoSize = true,
            Font = new Font("Segoe UI", 10F, FontStyle.Bold)
        };
        
        var descLabel = new Label
        {
            Text = feature.Description,
            Location = new Point(20, yPos + 25),
            AutoSize = true,
            Font = new Font("Segoe UI", 8F),
            ForeColor = Color.Gray
        };
        
        var toggle = new KtSwitch
        {
            Location = new Point(350, yPos + 10),
            Size = new Size(60, 30)
        };
        
        toggle.StateOn.Bg = feature.Color;
        toggle.StateOn.Thumb = KtColor.WHITE;
        toggle.StateOn.Border = feature.Color;
        
        this.Controls.Add(titleLabel);
        this.Controls.Add(descLabel);
        this.Controls.Add(toggle);
        
        yPos += 60;
    }
}
```

#### Privacy Settings

```csharp
private class PrivacySetting
{
    public string Title { get; set; }
    public string Description { get; set; }
    public bool DefaultValue { get; set; }
    public KtSwitch Switch { get; set; }
}

private void CreatePrivacySettings()
{
    var privacySettings = new List<PrivacySetting>
    {
        new PrivacySetting
        {
            Title = "Location Services",
            Description = "Allow apps to access your location",
            DefaultValue = true
        },
        new PrivacySetting
        {
            Title = "Camera Access",
            Description = "Allow apps to use your camera",
            DefaultValue = false
        },
        new PrivacySetting
        {
            Title = "Microphone Access",
            Description = "Allow apps to use your microphone",
            DefaultValue = false
        }
    };
    
    var panel = new Panel
    {
        Location = new Point(20, 20),
        Size = new Size(400, 250),
        AutoScroll = true
    };
    
    int yPos = 10;
    foreach (var setting in privacySettings)
    {
        var toggle = new KtSwitch
        {
            Location = new Point(330, yPos + 15),
            Size = new Size(60, 30),
            Checked = setting.DefaultValue
        };
        
        toggle.StateOn.Bg = KtColor.PRIMARY;
        toggle.StateOn.Thumb = KtColor.WHITE;
        
        var titleLabel = new Label
        {
            Text = setting.Title,
            Location = new Point(10, yPos + 10),
            AutoSize = true,
            Font = new Font("Segoe UI", 9.5F, FontStyle.Bold)
        };
        
        var descLabel = new Label
        {
            Text = setting.Description,
            Location = new Point(10, yPos + 35),
            AutoSize = true,
            Font = new Font("Segoe UI", 8F),
            ForeColor = Color.Gray
        };
        
        setting.Switch = toggle;
        
        panel.Controls.Add(toggle);
        panel.Controls.Add(titleLabel);
        panel.Controls.Add(descLabel);
        
        yPos += 70;
    }
    
    this.Controls.Add(panel);
}
```

#### Form with Multiple Switches

```csharp
public class SettingsForm : Form
{
    private Dictionary<string, KtSwitch> _switches;
    
    public SettingsForm()
    {
        InitializeComponent();
        CreateSwitches();
    }
    
    private void CreateSwitches()
    {
        _switches = new Dictionary<string, KtSwitch>
        {
            ["emailNotifications"] = CreateSwitch("Email Notifications", 20, true),
            ["pushNotifications"] = CreateSwitch("Push Notifications", 70, true),
            ["smsNotifications"] = CreateSwitch("SMS Notifications", 120, false),
            ["newsletter"] = CreateSwitch("Newsletter Subscription", 170, false)
        };
        
        foreach (var sw in _switches.Values)
        {
            sw.CheckedChanged += Switch_CheckedChanged;
            this.Controls.Add(sw);
        }
    }
    
    private KtSwitch CreateSwitch(string labelText, int yPosition, bool isChecked)
    {
        var label = new Label
        {
            Text = labelText,
            Location = new Point(20, yPosition + 5),
            AutoSize = true
        };
        
        var toggle = new KtSwitch
        {
            Location = new Point(300, yPosition),
            Size = new Size(60, 30),
            Checked = isChecked
        };
        
        this.Controls.Add(label);
        return toggle;
    }
    
    private void Switch_CheckedChanged(object sender, KtSwitch.CheckedChangedEventArgs e)
    {
        // Find which switch was toggled
        var toggledSwitch = (KtSwitch)sender;
        var switchName = _switches.FirstOrDefault(x => x.Value == toggledSwitch).Key;
        
        SaveSetting(switchName, e.Checked);
    }
    
    private void SaveSetting(string key, bool value)
    {
        // Save to settings/database
        Console.WriteLine($"{key} = {value}");
    }
}
```

***

### Advanced Features

#### Custom Animation Speed

```csharp
var fastSwitch = new KtSwitch
{
    Size = new Size(60, 30),
    Animation = 10  // Faster animation
};

var slowSwitch = new KtSwitch
{
    Size = new Size(60, 30),
    Animation = 2   // Slower animation
};
```

#### Custom Thumb Margin

```csharp
var tightSwitch = new KtSwitch
{
    Size = new Size(60, 30),
    ThumbMargin = 2  // Tight fit
};

var looseSwitch = new KtSwitch
{
    Size = new Size(60, 30),
    ThumbMargin = 8  // More spacing
};
```

#### Programmatic Control

```csharp
// Toggle the switch
toggle.Checked = !toggle.Checked;

// Set specific state
toggle.Value = true;

// Force refresh
toggle.Render();

// Resize and reposition
toggle.ResizeControl();
```

#### State-Based Styling

```csharp
var adaptiveSwitch = new KtSwitch
{
    Size = new Size(70, 35)
};

// OFF state - Gray/Disabled appearance
adaptiveSwitch.StateOff.Bg = KtColor.BASE_200;
adaptiveSwitch.StateOff.Thumb = KtColor.BASE_400;
adaptiveSwitch.StateOff.Border = KtColor.BASE_300;

// ON state - Success/Active appearance
adaptiveSwitch.StateOn.Bg = KtColor.SUCCESS;
adaptiveSwitch.StateOn.Thumb = KtColor.WHITE;
adaptiveSwitch.StateOn.Border = KtColor.SUCCESS;

adaptiveSwitch.CheckedChanged += (s, e) =>
{
    // Change appearance based on state
    if (e.Checked)
    {
        // Additional ON state logic
    }
    else
    {
        // Additional OFF state logic
    }
};
```

***

### Layout Patterns

#### TableLayoutPanel Integration

```csharp
private void CreateTableLayout()
{
    var tableLayout = new TableLayoutPanel
    {
        Location = new Point(20, 20),
        Size = new Size(400, 200),
        ColumnCount = 2,
        RowCount = 4
    };
    
    tableLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 70));
    tableLayout.ColumnStyles.Add(new ColumnStyle(SizeType.Percent, 30));
    
    var options = new[]
    {
        "Auto-Start",
        "Minimize to Tray",
        "Show Notifications",
        "Check for Updates"
    };
    
    for (int i = 0; i < options.Length; i++)
    {
        var label = new Label
        {
            Text = options[i],
            Dock = DockStyle.Fill,
            TextAlign = ContentAlignment.MiddleLeft
        };
        
        var toggle = new KtSwitch
        {
            Dock = DockStyle.Fill,
            Size = new Size(60, 30)
        };
        
        toggle.StateOn.Bg = KtColor.PRIMARY;
        toggle.StateOn.Thumb = KtColor.WHITE;
        
        tableLayout.Controls.Add(label, 0, i);
        tableLayout.Controls.Add(toggle, 1, i);
    }
    
    this.Controls.Add(tableLayout);
}
```

#### GroupBox with Switches

```csharp
private GroupBox CreateSwitchGroup(string title, Dictionary<string, bool> options)
{
    var groupBox = new GroupBox
    {
        Text = title,
        Size = new Size(300, 40 + (options.Count * 45)),
        Padding = new Padding(10)
    };
    
    int yPos = 25;
    foreach (var option in options)
    {
        var label = new Label
        {
            Text = option.Key,
            Location = new Point(10, yPos + 5),
            AutoSize = true
        };
        
        var toggle = new KtSwitch
        {
            Location = new Point(220, yPos),
            Size = new Size(60, 30),
            Checked = option.Value
        };
        
        groupBox.Controls.Add(label);
        groupBox.Controls.Add(toggle);
        
        yPos += 45;
    }
    
    return groupBox;
}

// Usage
var displayGroup = CreateSwitchGroup("Display Options", new Dictionary<string, bool>
{
    ["Dark Mode"] = false,
    ["High Contrast"] = false,
    ["Large Text"] = false
});

this.Controls.Add(displayGroup);
```

***

### Validation and State Management

```csharp
public class PreferencesManager
{
    private Dictionary<string, KtSwitch> _preferences = new Dictionary<string, KtSwitch>();
    
    public void AddPreference(string key, KtSwitch toggle)
    {
        _preferences[key] = toggle;
        toggle.CheckedChanged += (s, e) => SavePreference(key, e.Checked);
    }
    
    public bool GetPreference(string key)
    {
        return _preferences.ContainsKey(key) && _preferences[key].Checked;
    }
    
    public void SetPreference(string key, bool value)
    {
        if (_preferences.ContainsKey(key))
        {
            _preferences[key].Checked = value;
        }
    }
    
    public Dictionary<string, bool> GetAllPreferences()
    {
        return _preferences.ToDictionary(
            kvp => kvp.Key,
            kvp => kvp.Value.Checked
        );
    }
    
    private void SavePreference(string key, bool value)
    {
        // Save to settings file, database, etc.
        Properties.Settings.Default[key] = value;
        Properties.Settings.Default.Save();
    }
    
    public void LoadPreferences()
    {
        foreach (var pref in _preferences)
        {
            try
            {
                pref.Value.Checked = (bool)Properties.Settings.Default[pref.Key];
            }
            catch
            {
                // Use default value
            }
        }
    }
}

// Usage
var prefManager = new PreferencesManager();
prefManager.AddPreference("darkMode", darkModeSwitch);
prefManager.AddPreference("notifications", notificationSwitch);
prefManager.LoadPreferences();
```

***

### Conditional Logic

```csharp
private void CreateConditionalSwitches()
{
    var masterSwitch = new KtSwitch
    {
        Location = new Point(20, 20),
        Size = new Size(60, 30)
    };
    
    var childSwitch1 = new KtSwitch
    {
        Location = new Point(40, 70),
        Size = new Size(60, 30),
        Enabled = false
    };
    
    var childSwitch2 = new KtSwitch
    {
        Location = new Point(40, 120),
        Size = new Size(60, 30),
        Enabled = false
    };
    
    // Master switch controls child switches
    masterSwitch.CheckedChanged += (s, e) =>
    {
        childSwitch1.Enabled = e.Checked;
        childSwitch2.Enabled = e.Checked;
        
        if (!e.Checked)
        {
            childSwitch1.Checked = false;
            childSwitch2.Checked = false;
        }
    };
    
    var masterLabel = new Label
    {
        Text = "Enable Advanced Features",
        Location = new Point(90, 25),
        AutoSize = true,
        Font = new Font("Segoe UI", 10F, FontStyle.Bold)
    };
    
    var child1Label = new Label
    {
        Text = "Sub-feature 1",
        Location = new Point(110, 75),
        AutoSize = true
    };
    
    var child2Label = new Label
    {
        Text = "Sub-feature 2",
        Location = new Point(110, 125),
        AutoSize = true
    };
    
    this.Controls.AddRange(new Control[]
    {
        masterSwitch, masterLabel,
        childSwitch1, child1Label,
        childSwitch2, child2Label
    });
}
```

***

### Design Tips

1. **Size Guidelines**: Standard switch size is 60x30, but can be adjusted proportionally
2. **Animation Speed**: Use 3-8 for smooth animations; higher values are faster
3. **Thumb Margin**: Typically 3-5px for proper visual spacing
4. **Color Contrast**: Ensure ON and OFF states are clearly distinguishable
5. **Border Radius**: Set to half the height for pill-shaped switches
6. **State Consistency**: Use consistent colors across similar switches
7. **Label Placement**: Place labels to the left or right, maintaining alignment
8. **Disabled State**: The control automatically adjusts opacity when disabled

***

### Accessibility Features

* Automatic cursor change to hand pointer
* Click anywhere on the switch to toggle
* Smooth animation provides visual feedback
* Clear visual distinction between ON/OFF states
* Disabled state is visually apparent
* Keyboard accessibility through standard focus/click patterns

***

### Performance Notes

* Animation uses a timer for smooth transitions
* Thumb position calculated dynamically on resize
* Graphics rendered using GDI+ for quality
* Control automatically cleans up resources on disposal

***

### Size Recommendations

| Use Case  | Recommended Size | Thumb Margin |
| --------- | ---------------- | ------------ |
| Standard  | 60x30            | 5            |
| Compact   | 50x25            | 3            |
| Large     | 70x35            | 6            |
| iOS Style | 55x30            | 3            |
| Material  | 50x25            | 2            |

***

### Migration Notes

If migrating from CheckBox:

```csharp
// Standard CheckBox
var oldCheckbox = new CheckBox
{
    Text = "Enable Feature",
    Location = new Point(20, 20),
    Checked = true
};

// KtSwitch equivalent (with separate label)
var label = new Label
{
    Text = "Enable Feature",
    Location = new Point(90, 25),
    AutoSize = true
};

var newSwitch = new KtSwitch
{
    Location = new Point(20, 20),
    Size = new Size(60, 30),
    Checked = true
};

newSwitch.StateOn.Bg = KtColor.PRIMARY;
newSwitch.StateOn.Thumb = KtColor.WHITE;
```

***

### Best Practices

1. **Use for Binary Choices**: Switches work best for settings that take effect immediately
2. **Provide Clear Labels**: Always accompany switches with descriptive labels
3. **Group Related Switches**: Organize related toggles in panels or groups
4. **Feedback on Change**: Show confirmation or apply changes immediately
5. **Disabled State**: Use when options are unavailable but should remain visible
6. **Consistent Positioning**: Align switches vertically or use consistent spacing
7. **State Persistence**: Save switch states to user preferences
8. **Visual Hierarchy**: Use size and color to indicate importance
