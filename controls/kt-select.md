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

# 🔹 Kt-Select

### Overview

**KtSelect** is a beautifully crafted, theme-intelligent dropdown control from the KimTools.WinForms SDK that transforms standard item selection into an elegant user experience. Featuring automatic theme adaptation, extensive customization options, and smooth visual transitions, KtSelect elevates the traditional Windows Forms ComboBox to match modern design standards.

#### Why Choose KtSelect?

* **🎨 Theme Intelligence**: Automatically adapts to light/dark themes without code changes
* **✨ Modern Aesthetics**: Rounded corners, smooth borders, and polished visuals
* **🎯 Flexible Positioning**: Position indicator arrows left, right, or hide them entirely
* **🌈 Rich Customization**: Control every color from idle to hover to disabled states
* **⚡ High Performance**: Optimized rendering with anti-aliasing and double-buffering
* **♿ Accessibility**: Clear visual states and keyboard navigation support

#### Perfect For

* Modern application forms and settings panels
* Dropdown menus with branded color schemes
* Status selectors with visual feedback
* Category and filter pickers
* Any UI requiring elegant item selection
* Applications with light/dark theme support

***

### Quick Start

```csharp
// Create a simple, elegant dropdown
var dropdown = new KtSelect
{
    Width = 250,
    Height = 40,
    BorderRadius = 8
};

dropdown.Items.AddRange(new[] { "Option 1", "Option 2", "Option 3" });
dropdown.SelectedIndex = 0;

// Handle selection changes
dropdown.SelectedIndexChanged += (s, e) =>
{
    MessageBox.Show($"Selected: {dropdown.Text}");
};
```

***

### Properties Reference

#### 🎨 Appearance Properties

| Property                    | Type              | Default         | Description                                |
| --------------------------- | ----------------- | --------------- | ------------------------------------------ |
| **Bg**                      | `KtColor`         | `PRIMARY`       | Background color of the dropdown button    |
| **BorderColor**             | `KtColor`         | `PRIMARY % 50`  | Border color when control is enabled       |
| **BorderRadius**            | `int`             | `1`             | Corner radius in pixels (auto-constrained) |
| **DropdownBorderThickness** | `BorderThickness` | `Thick`         | Border width - Thin (1px) or Thick (2px)   |
| **TextColor**               | `KtColor`         | `!PRIMARY`      | Color of the displayed text                |
| **Font**                    | `Font`            | `Segoe UI, 9pt` | Font used for text rendering               |

#### 🔽 Indicator Properties

| Property               | Type         | Default    | Description                                 |
| ---------------------- | ------------ | ---------- | ------------------------------------------- |
| **IndicatorColor**     | `KtColor`    | `!PRIMARY` | Color of the dropdown arrow                 |
| **IndicatorAlignment** | `Indicator`  | `Right`    | Arrow position - Left, Right, or None       |
| **FillIndicator**      | `bool`       | `false`    | Fill the indicator triangle or draw outline |
| **Direction**          | `Directions` | `Down`     | Arrow direction - Up or Down                |

#### 📋 Item Properties

| Property                   | Type      | Default     | Description                              |
| -------------------------- | --------- | ----------- | ---------------------------------------- |
| **ItemBackColor**          | `KtColor` | `BASE`      | Background color of list items           |
| **ItemForeColor**          | `KtColor` | `!BASE`     | Text color of list items                 |
| **ItemBorderColor**        | `KtColor` | `BASE % 50` | Border color around the dropdown list    |
| **ItemHighLightColor**     | `KtColor` | `PRIMARY`   | Background when item is selected/hovered |
| **ItemHighLightForeColor** | `KtColor` | `!PRIMARY`  | Text color when item is highlighted      |
| **ItemHeight**             | `int`     | `15` (min)  | Height of each item in the list          |
| **ItemTopMargin**          | `int`     | `1`         | Vertical spacing between items           |

#### 🚫 Disabled State Properties

| Property                   | Type      | Default      | Description                         |
| -------------------------- | --------- | ------------ | ----------------------------------- |
| **DisabledBackColor**      | `KtColor` | `Gray`       | Background when control is disabled |
| **DisabledBorderColor**    | `KtColor` | `Gray % 50`  | Border color when disabled          |
| **DisabledForeColor**      | `KtColor` | `White`      | Text color when disabled            |
| **DisabledIndicatorColor** | `KtColor` | `WhiteSmoke` | Arrow color when disabled           |

#### 📐 Layout Properties

| Property           | Type        | Default  | Description                                  |
| ------------------ | ----------- | -------- | -------------------------------------------- |
| **TextAlignment**  | `TextAlign` | `Left`   | Text alignment - Left, Center, or Right      |
| **TextLeftMargin** | `int`       | `5`      | Horizontal padding for text                  |
| **Width**          | `int`       | (varies) | Width of the control                         |
| **Height**         | `int`       | (varies) | Height of the control (also sets ItemHeight) |

#### 📊 Data Properties

| Property          | Type               | Default | Description                            |
| ----------------- | ------------------ | ------- | -------------------------------------- |
| **Items**         | `ObjectCollection` | (empty) | Collection of selectable items         |
| **Text**          | `string`           | `""`    | Currently displayed/selected text      |
| **SelectedIndex** | `int`              | `-1`    | Index of the selected item             |
| **Enabled**       | `bool`             | `true`  | Whether the control accepts user input |

***

### Events

| Event                    | When It Fires                      | Use Case                                     |
| ------------------------ | ---------------------------------- | -------------------------------------------- |
| **SelectedIndexChanged** | When user selects a different item | Update UI, save preferences, trigger actions |
| **DropDown**             | When dropdown list opens           | Load dynamic data, adjust position           |
| **DropDownClosed**       | When dropdown list closes          | Validate selection, save state               |

***

### Enumerations

#### BorderThickness

```csharp
public enum BorderThickness
{
    Thick,  // 2-pixel border
    Thin    // 1-pixel border
}
```

#### Indicator

```csharp
public enum Indicator
{
    Left,   // Arrow on left, text right-aligned
    Right,  // Arrow on right, text left-aligned
    None    // No arrow, custom text alignment
}
```

#### TextAlign

```csharp
public enum TextAlign
{
    Left,    // Left-aligned text
    Center,  // Centered text
    Right    // Right-aligned text
}
```

#### Directions

```csharp
public enum Directions
{
    Down,  // Arrow points downward (default)
    Up     // Arrow points upward
}
```

***

### Real-World Examples

#### 1. Country Selector with Flag Icons

```csharp
var countryDropdown = new KtSelect
{
    Width = 280,
    Height = 42,
    BorderRadius = 10,
    Bg = KtColor.Base,
    BorderColor = KtColor.Primary % 30,
    ItemHighLightColor = KtColor.Primary % 15,
    Font = new Font("Segoe UI", 10)
};

countryDropdown.Items.AddRange(new[] 
{ 
    "🇰🇪 Kenya",
    "🇺🇬 Uganda", 
    "🇹🇿 Tanzania",
    "🇷🇼 Rwanda",
    "🇧🇮 Burundi"
});

countryDropdown.SelectedIndex = 0;
```

#### 2. Status Selector with Dynamic Colors

```csharp
var statusDropdown = new KtSelect
{
    Width = 200,
    Height = 38,
    BorderRadius = 8,
    FillIndicator = true
};

statusDropdown.Items.AddRange(new[] 
{ 
    "Active", 
    "Pending", 
    "Completed", 
    "Failed" 
});

// Change colors based on selection
statusDropdown.SelectedIndexChanged += (s, e) =>
{
    switch (statusDropdown.SelectedIndex)
    {
        case 0: // Active
            statusDropdown.Bg = KtColor.Green;
            statusDropdown.TextColor = KtColor.White;
            statusDropdown.IndicatorColor = KtColor.White;
            break;
        case 1: // Pending
            statusDropdown.Bg = KtColor.Yellow;
            statusDropdown.TextColor = KtColor.Black;
            statusDropdown.IndicatorColor = KtColor.Black;
            break;
        case 2: // Completed
            statusDropdown.Bg = KtColor.Blue;
            statusDropdown.TextColor = KtColor.White;
            statusDropdown.IndicatorColor = KtColor.White;
            break;
        case 3: // Failed
            statusDropdown.Bg = KtColor.Red;
            statusDropdown.TextColor = KtColor.White;
            statusDropdown.IndicatorColor = KtColor.White;
            break;
    }
};
```

#### 3. Minimalist Design (No Border, Centered)

```csharp
var minimalistDropdown = new KtSelect
{
    Width = 180,
    Height = 40,
    BorderRadius = 20, // Pill shape
    IndicatorAlignment = KtSelect.Indicator.None,
    TextAlignment = KtSelect.TextAlign.Center,
    Bg = KtColor.Primary % 10,
    BorderColor = Color.Transparent,
    TextColor = KtColor.Primary,
    Font = new Font("Segoe UI Semibold", 10)
};

minimalistDropdown.Items.AddRange(new[] { "Small", "Medium", "Large" });
```

#### 4. Material Design Style

```csharp
var materialDropdown = new KtSelect
{
    Width = 260,
    Height = 44,
    BorderRadius = 4,
    DropdownBorderThickness = KtSelect.BorderThickness.Thin,
    Bg = KtColor.Base,
    BorderColor = KtColor.Gray % 40,
    ItemHighLightColor = KtColor.Primary % 12,
    ItemTopMargin = 2,
    TextLeftMargin = 16,
    Font = new Font("Roboto", 10)
};
```

#### 5. Left-Aligned Indicator (Unusual Layout)

```csharp
var leftIndicatorDropdown = new KtSelect
{
    Width = 220,
    Height = 38,
    IndicatorAlignment = KtSelect.Indicator.Left,
    // TextAlignment automatically becomes Right
    BorderRadius = 8,
    TextLeftMargin = 12,
    FillIndicator = true
};
```

#### 6. Premium Styled Selector

```csharp
var premiumDropdown = new KtSelect
{
    Width = 300,
    Height = 48,
    BorderRadius = 12,
    DropdownBorderThickness = KtSelect.BorderThickness.Thick,
    Bg = KtColor.Primary,
    BorderColor = KtColor.Primary,
    TextColor = KtColor.White,
    IndicatorColor = KtColor.White,
    ItemBackColor = KtColor.Base,
    ItemForeColor = KtColor.Primary,
    ItemHighLightColor = KtColor.Primary % 20,
    ItemHighLightForeColor = KtColor.Primary,
    FillIndicator = true,
    Font = new Font("Segoe UI Semibold", 11)
};

premiumDropdown.Items.AddRange(new[] 
{ 
    "Premium Plan - $99/mo",
    "Business Plan - $49/mo",
    "Starter Plan - $19/mo"
});
```

#### 7. Cascading Dropdowns (Parent-Child)

```csharp
var categoryDropdown = new KtSelect
{
    Location = new Point(20, 20),
    Width = 220,
    Height = 40,
    BorderRadius = 8
};
categoryDropdown.Items.AddRange(new[] { "Electronics", "Clothing", "Books" });

var subcategoryDropdown = new KtSelect
{
    Location = new Point(20, 75),
    Width = 220,
    Height = 40,
    BorderRadius = 8,
    Enabled = false
};

// Populate subcategories based on category
categoryDropdown.SelectedIndexChanged += (s, e) =>
{
    subcategoryDropdown.Items.Clear();
    subcategoryDropdown.Enabled = true;
    
    switch (categoryDropdown.Text)
    {
        case "Electronics":
            subcategoryDropdown.Items.AddRange(new[] 
            { "Phones", "Laptops", "Tablets", "Accessories" });
            break;
        case "Clothing":
            subcategoryDropdown.Items.AddRange(new[] 
            { "Shirts", "Pants", "Dresses", "Shoes" });
            break;
        case "Books":
            subcategoryDropdown.Items.AddRange(new[] 
            { "Fiction", "Non-Fiction", "Comics", "Textbooks" });
            break;
    }
    
    subcategoryDropdown.SelectedIndex = 0;
};
```

#### 8. Form Settings Panel

```csharp
// Theme selector
var themeDropdown = new KtSelect
{
    Location = new Point(120, 20),
    Width = 200,
    Height = 38,
    BorderRadius = 8
};
themeDropdown.Items.AddRange(new[] { "System", "Light", "Dark" });
themeDropdown.SelectedIndex = 0;

// Language selector
var languageDropdown = new KtSelect
{
    Location = new Point(120, 70),
    Width = 200,
    Height = 38,
    BorderRadius = 8
};
languageDropdown.Items.AddRange(new[] { "English", "Español", "Français" });
languageDropdown.SelectedIndex = 0;

// Font size selector
var fontSizeDropdown = new KtSelect
{
    Location = new Point(120, 120),
    Width = 200,
    Height = 38,
    BorderRadius = 8
};
fontSizeDropdown.Items.AddRange(new[] { "Small", "Medium", "Large" });
fontSizeDropdown.SelectedIndex = 1;

// Apply button
var applyButton = new Button
{
    Text = "Apply Settings",
    Location = new Point(120, 170),
    Width = 200,
    Height = 38
};

applyButton.Click += (s, e) =>
{
    // Save settings
    SaveSetting("Theme", themeDropdown.Text);
    SaveSetting("Language", languageDropdown.Text);
    SaveSetting("FontSize", fontSizeDropdown.Text);
};
```

#### 9. Disabled State Styling

```csharp
var disabledDropdown = new KtSelect
{
    Width = 240,
    Height = 40,
    BorderRadius = 8,
    Enabled = false,
    DisabledBackColor = KtColor.Gray % 15,
    DisabledBorderColor = KtColor.Gray % 25,
    DisabledForeColor = KtColor.Gray % 60,
    DisabledIndicatorColor = KtColor.Gray % 50
};

disabledDropdown.Items.AddRange(new[] 
{ 
    "Feature Coming Soon",
    "Not Available in Trial"
});

// Enable after user upgrades
var upgradeButton = new Button { Text = "Upgrade to Enable" };
upgradeButton.Click += (s, e) =>
{
    disabledDropdown.Enabled = true;
};
```

#### 10. High-Contrast Accessibility Mode

```csharp
var accessibleDropdown = new KtSelect
{
    Width = 260,
    Height = 44,
    BorderRadius = 6,
    DropdownBorderThickness = KtSelect.BorderThickness.Thick,
    Bg = KtColor.White,
    BorderColor = KtColor.Black,
    TextColor = KtColor.Black,
    IndicatorColor = KtColor.Black,
    ItemBackColor = KtColor.White,
    ItemForeColor = KtColor.Black,
    ItemHighLightColor = KtColor.Black,
    ItemHighLightForeColor = KtColor.White,
    ItemBorderColor = KtColor.Black,
    Font = new Font("Arial", 11, FontStyle.Bold)
};
```

***

### Advanced Features

#### 🎯 Smart Indicator-Text Coupling

KtSelect automatically adjusts text alignment based on indicator position:

```csharp
// Setting indicator position automatically adjusts text alignment
dropdown.IndicatorAlignment = Indicator.Right;  
// → TextAlignment becomes Left

dropdown.IndicatorAlignment = Indicator.Left;   
// → TextAlignment becomes Right

dropdown.IndicatorAlignment = Indicator.None;   
// → You control TextAlignment manually
```

#### 🔒 Auto-Constrained Border Radius

Border radius intelligently adjusts to prevent visual overflow:

```csharp
// If you set radius too high for the control height,
// it's automatically constrained to maintain visual quality
dropdown.BorderRadius = 50;  // Too high for 40px height
// → Automatically adjusted to appropriate maximum
```

#### 🌈 KtColor Integration

All color properties use the powerful `KtColor` system:

```csharp
// Theme-aware colors
dropdown.Bg = KtColor.Primary;           // Uses theme's primary color
dropdown.BorderColor = KtColor.Primary % 50;  // 50% lighter/darker
dropdown.TextColor = !KtColor.Primary;   // Inverted for contrast

// Automatic theme adaptation
// When user switches light/dark mode, all colors update automatically!
```

See [KtColor Documentation](https://www.kimtoo.net/sdk/utilities/kt-color) for color operations.

***

### Best Practices

#### ✅ Do's

1. **Use consistent heights** - Keep dropdowns 36-44px for familiarity
2. **Maintain contrast** - Ensure text is readable against backgrounds
3. **Set appropriate margins** - Use 1-4px for `ItemTopMargin`
4. **Choose readable fonts** - Stick to UI fonts like Segoe UI, Roboto
5. **Test both themes** - Verify appearance in light and dark modes
6. **Handle selection events** - Always respond to `SelectedIndexChanged`
7. **Configure disabled states** - Set disabled colors for accessibility
8. **Use semantic colors** - Green for success, Red for errors, etc.
9. **Keep border radius proportional** - Typically 20-30% of height
10. **Provide feedback** - Use visual changes to confirm selections

#### ❌ Don'ts

1. **Don't use extreme colors** - Avoid eye-strain with balanced palettes
2. **Don't make items too small** - Minimum 15px height for usability
3. **Don't over-customize** - Maintain consistency across your app
4. **Don't forget disabled states** - Users need visual feedback
5. **Don't ignore contrast ratios** - Follow WCAG guidelines
6. **Don't mix design styles** - Be consistent with Material/Fluent/Custom
7. **Don't overcrowd items** - Leave breathing room with proper margins
8. **Don't use unclear labels** - Keep item text descriptive
9. **Don't hardcode colors** - Use KtColor for theme support
10. **Don't skip event handlers** - Handle selection changes appropriately

***

### Performance Tips

* **Reuse instances** - Don't create new dropdowns repeatedly
* **Lazy load items** - Populate on `DropDown` event for large lists
* **Dispose properly** - Always dispose when removing from forms
* **Batch updates** - Use `BeginUpdate()`/`EndUpdate()` for multiple changes
* **Cache selections** - Store SelectedIndex to avoid unnecessary lookups

***

### Troubleshooting

#### Items not showing?

```csharp
// Ensure items are added correctly
dropdown.Items.Clear();
dropdown.Items.AddRange(new[] { "Item 1", "Item 2" });
```

#### Colors not updating?

```csharp
// Call Refresh() after property changes
dropdown.BorderColor = KtColor.Blue;
dropdown.Refresh();
```

#### Text not aligning correctly?

```csharp
// Check TextLeftMargin and TextAlignment
dropdown.TextLeftMargin = 10;
dropdown.TextAlignment = KtSelect.TextAlign.Left;
```

#### Indicator not visible?

```csharp
// Ensure IndicatorAlignment is not None
dropdown.IndicatorAlignment = KtSelect.Indicator.Right;
dropdown.FillIndicator = true; // Makes it more visible
```

***
