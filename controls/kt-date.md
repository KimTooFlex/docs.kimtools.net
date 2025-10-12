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

# 🔹 Kt-Date



### Overview

**KT Date** is a beautifully customizable date picker control for WinForms applications. It transforms the standard DateTimePicker into a modern, stylish component with advanced styling capabilities including gradient backgrounds, customizable borders, smooth squircle shapes, and flexible text alignment. Perfect for creating polished, professional-looking date selection interfaces in your .NET applications.

### Use Cases

* **Modern Forms**: Create sleek, contemporary data entry forms with styled date inputs
* **Dashboard Applications**: Build visually consistent date filters and selectors with gradient backgrounds
* **Reporting Tools**: Add elegant date range pickers for report generation
* **Scheduling Systems**: Design intuitive appointment and event date selectors
* **Data Management**: Enhance CRUD forms with professional-looking date fields
* **Theme-Aware Apps**: Automatically adapt to light/dark themes with KT Color integration

***

### Key Features

✨ **Advanced Styling**

* **Squircle Shapes**: Smooth, iOS-style rounded corners with percentage-based radius (0.0-0.99) or pixel values
* **Gradient Backgrounds**: Full [KT Brush](https://www.kimtoo.net/sdk/utilities/kt-brush) support for solid colors, linear/radial gradients
* **Customizable Borders**: Adjustable color, width, and independent border styling
* **Transparent Backgrounds**: Seamlessly blend with any parent container

🎨 **Flexible Layout**

* Icon positioning (left, right, or none)
* Text alignment options (left, center, right)
* Adjustable text margins
* Responsive sizing

🌙 **Theme Intelligence**

* Automatic theme change detection via [KT Color](https://www.kimtoo.net/sdk/utilities/kt-color)
* Disabled state styling
* Smart color fallbacks and inheritance

📅 **Enhanced Functionality**

* Optional week number display
* Auto-sizing dropdown calendar&#x20;

***

### Properties Reference

| Property               | Type      | Default | Description                                                              |
| ---------------------- | --------- | ------- | ------------------------------------------------------------------------ |
| **Background**         | KtBrush   | None    | Sets the background using solid colors, gradients, or patterns           |
| **Border**             | KtColor   | Empty   | Sets the border color                                                    |
| **BorderRadius**       | float?    | 0.5     | Border radius (0.0-0.99 = percentage, ≥1 = pixels, null = fully rounded) |
| **BorderWidth**        | float     | 1.5     | Border thickness in pixels                                               |
| **TextAlign**          | TextAlign | Left    | Aligns date text (Left, Center, Right)                                   |
| **DisplayWeekNumbers** | bool      | false   | Shows week numbers in dropdown calendar                                  |
| Icon                   | Image     | null    | Custom Icon Image                                                        |
| **IconColor**          | KtColor   | Empty   | Calendar icon color                                                      |
| **IconAlign**          | Indicator | Right   | Icon position (Left, Right, None)                                        |
| **TextMargin**         | int       | 8       | Left padding for text                                                    |
| **TextColor**          | KtColor   | Empty   | Date text color                                                          |

***

### Usage Examples

#### Example 1: Modern Squircle Date Picker

```csharp
var datePicker = new KtDate();
datePicker.Background = new KtBrush(KtColor.Primary);
datePicker.Border = KtColor.Primary;
datePicker.BorderRadius = 0.5f; // 50% rounded (squircle)
datePicker.BorderWidth = 2f;
datePicker.TextColor = KtColor.White;
datePicker.IconColor = KtColor.White;
datePicker.Height = 44;
```

#### Example 2: Gradient Background Style

```csharp
var datePicker = new KtDate();

// Create linear gradient background
var gradientBrush = new KtBrush();
gradientBrush.Type = KtBrush.BrushType.LinearGradient;
gradientBrush.GradientStops = new[] 
{
    new KtBrush.GradientStop(KtColor.Info, 0f),
    new KtBrush.GradientStop(KtColor.Primary, 1f)
};

datePicker.Background = gradientBrush;
datePicker.BorderRadius = 12f; // 12px radius
datePicker.BorderWidth = 0f; // No border
datePicker.TextColor = KtColor.White;
datePicker.IconColor = KtColor.White;
```

#### Example 3: Outlined Style (Border Only)

```csharp
var datePicker = new KtDate();
datePicker.Background = KtBrush.None; // Transparent background
datePicker.Border = KtColor.Neutral;
datePicker.BorderWidth = 1.5f;
datePicker.BorderRadius = 8f;
datePicker.TextColor = KtColor.Neutral;
datePicker.IconColor = KtColor.Neutral;
datePicker.Height = 40;
```

#### Example 4: Pill-Shaped Design

```csharp
var datePicker = new KtDate();
datePicker.Background = new KtBrush(KtColor.Success);
datePicker.BorderRadius = null; // Fully rounded (pill shape)
datePicker.BorderWidth = 0f;
datePicker.TextColor = KtColor.White;
datePicker.IconColor = KtColor.White;
datePicker.Height = 36;
datePicker.Width = 200;
```

#### Example 5: Minimalist Centered Design

```csharp
var datePicker = new KtDate();
datePicker.IconLocation = KtDate.Indicator.None;
datePicker.DateTextAlign = KtDate.TextAlign.Center;
datePicker.Background = new KtBrush(KtColor.Surface);
datePicker.Border = KtColor.Border;
datePicker.BorderRadius = 6f;
datePicker.BorderWidth = 1f;
datePicker.TextMargin = 20;
```

#### Example 6: With Week Numbers

```csharp
var datePicker = new KtDate();
datePicker.DisplayWeekNumbers = true;
datePicker.Background = new KtBrush(KtColor.White);
datePicker.Border = KtColor.Primary;
datePicker.BorderRadius = 10f;
datePicker.BorderWidth = 2f;
datePicker.Width = 280; // Wider for week numbers
datePicker.TextColor = KtColor.Neutral;
```

#### Example 7: Radial Gradient Effect

```csharp
var datePicker = new KtDate();

// Create radial gradient
var radialBrush = new KtBrush();
radialBrush.Type = KtBrush.BrushType.RadialGradient;
radialBrush.GradientStops = new[]
{
    new KtBrush.GradientStop(KtColor.Warning, 0f),
    new KtBrush.GradientStop(KtColor.Danger, 1f)
};

datePicker.Background = radialBrush;
datePicker.BorderRadius = 0.7f; // 70% rounded
datePicker.TextColor = KtColor.White;
datePicker.IconColor = KtColor.White;
```

#### Example 8: Disabled State

```csharp
var datePicker = new KtDate();
datePicker.Background = new KtBrush(KtColor.Surface);
datePicker.Border = KtColor.Border;
datePicker.DisabledColor = KtColor.Disabled;
datePicker.BorderRadius = 8f;
datePicker.Enabled = false; // Shows DisabledColor
```

***

### Understanding Border Radius

KT Date uses an intelligent **squircle** algorithm for smooth, modern corners:

#### Percentage Mode (0.0 - 0.99)

Values between 0 and 0.99 are treated as **percentages of control height**:

* `0.0` = Sharp corners (0% rounded)
* `0.25` = 25% rounded (subtle curves)
* `0.5` = 50% rounded (balanced squircle) ⭐ **Default**
* `0.75` = 75% rounded (very smooth)
* `0.99` = 99% rounded (nearly circular)

#### Pixel Mode (≥ 1.0)

Values of 1.0 or greater are treated as **pixel measurements**:

* `1f` = 1px corner radius
* `8f` = 8px corner radius
* `16f` = 16px corner radius

#### Fully Rounded (null)

Setting `BorderRadius = null` creates a **perfect pill shape** (100% rounded ends).

***

### Design Guidelines

#### Border Radius Best Practices

**For Modern Apps (Recommended)**

```csharp
BorderRadius = 0.5f; // Squircle shape, iOS-style
BorderRadius = 0.6f; // Smoother curves
```

**For Traditional Apps**

```csharp
BorderRadius = 4f;   // Subtle 4px radius
BorderRadius = 8f;   // Standard 8px radius
```

**For Pill Buttons**

```csharp
BorderRadius = null; // Fully rounded ends
```

#### Background Styling Tips

1. **Solid Backgrounds**: Use `new KtBrush(KtColor.Primary)` for simple, flat designs
2. **Gradients**: Create depth with linear or radial gradients
3. **Transparent**: Set `Background = KtBrush.None` for outline-only styles
4. **Contrast**: Ensure text remains readable against background

#### Icon Positioning Strategy

* **Right (Default)**: Best for LTR languages, text flows naturally
* **Left**: Better for RTL layouts or right-aligned forms
* **None**: Cleaner, minimalist look when icon isn't needed

#### Sizing Recommendations

| Use Case          | Height  | Width     |
| ----------------- | ------- | --------- |
| Compact Forms     | 32-36px | 180-200px |
| Standard Forms    | 40-44px | 220-250px |
| Touch-Friendly    | 48-52px | 250-280px |
| With Week Numbers | Any     | 280-320px |

***

### Advanced Features

#### KT Brush Integration

KT Date fully supports [KT Brush](https://www.kimtoo.net/sdk/utilities/kt-brush) for advanced background rendering:

* **Solid Colors**: Single-color fills
* **Linear Gradients**: Horizontal, vertical, or diagonal color transitions
* **Radial Gradients**: Circular color spreads from center
* **Pattern Fills**: Custom brush patterns (when supported)

```csharp
// Example: Diagonal gradient
var brush = new KtBrush();
brush.Type = KtBrush.BrushType.LinearGradient;
brush.Angle = 45; // Diagonal
brush.GradientStops = new[]
{
    new KtBrush.GradientStop(KtColor.Info, 0f),
    new KtBrush.GradientStop(KtColor.Success, 1f)
};
datePicker.Background = brush;
```

#### Theme-Aware Rendering

KT Date automatically responds to system theme changes through [KT Color](https://www.kimtoo.net/sdk/utilities/kt-color):

```csharp
// Colors auto-adjust when theme changes
datePicker.Border = KtColor.Border;        // Adapts to theme
datePicker.TextColor = KtColor.Content;    // Auto-adjusts
datePicker.Background = new KtBrush(KtColor.Surface);
```

#### Auto-Sizing Calendar Dropdown

The dropdown calendar automatically:

* Matches the control width
* Adjusts for week numbers display
* Optimizes height for best viewing
* Respects `DisplayWeekNumbers` property

#### High-Quality Graphics

Built with:

* **Anti-aliasing**: Smooth edges at any size
* **High-quality interpolation**: Crisp icon rendering
* **Double-buffering**: Flicker-free updates
* **DPI awareness**: Sharp rendering on high-DPI displays

***

### Methods

#### Render()

Manually refreshes the control's appearance. Useful when programmatically changing multiple properties:

```csharp
datePicker.Border = KtColor.Primary;
datePicker.Background = new KtBrush(KtColor.Info);
datePicker.BorderRadius = 10f;
datePicker.Render(); // Force refresh
```

#### ✅ Do's

* **Use squircle mode** (0.5f) for modern, iOS-like aesthetics
* **Leverage KT Color** for automatic theme adaptation
* **Set appropriate heights** (minimum 32px for accessibility)
* **Use gradients sparingly** for visual interest without overwhelming
* **Test disabled states** to ensure clear visual feedback
* **Match styling** across all date pickers in your form

#### ❌ Don'ts

* **Avoid extreme radius values** that don't match control height
* **Don't mix design styles** (squircle vs sharp corners) in one form
* **Don't sacrifice contrast** for aesthetics - readability first
* **Avoid overly complex gradients** with too many color stops
* **Don't forget disabled styling** - always set `DisabledColor`

***

### Common Patterns

#### Pattern 1: Form Input Style

```csharp
// Clean, professional form input
datePicker.Background = new KtBrush(KtColor.White);
datePicker.Border = KtColor.Border;
datePicker.BorderRadius = 8f;
datePicker.BorderWidth = 1f;
datePicker.TextColor = KtColor.Content;
```

#### Pattern 2: Accent Button Style

```csharp
// Prominent, colorful date selector
datePicker.Background = new KtBrush(KtColor.Primary);
datePicker.BorderRadius = 0.5f;
datePicker.BorderWidth = 0f;
datePicker.TextColor = KtColor.White;
datePicker.IconColor = KtColor.White;
```

#### Pattern 3: Minimal Outline

```csharp
// Lightweight, unobtrusive
datePicker.Background = KtBrush.None;
datePicker.Border = KtColor.Border;
datePicker.BorderRadius = 6f;
datePicker.BorderWidth = 1f;
```

***

### Troubleshooting

**Q: My border radius isn't working as expected**

* Check if you're using percentage mode (0.0-0.99) or pixel mode (≥1.0)
* Ensure control height accommodates the radius value
* Try `BorderRadius = 0.5f` for reliable squircle shape

**Q: Background gradient isn't showing**

* Verify `Background` is set to a KtBrush with gradient configuration
* Check that gradient stops are properly defined
* Ensure `BorderWidth > 0` if you want both border and background

**Q: Icon color not changing**

* Set `IconColor` property explicitly
* If using `KtColor.Empty`, icon inherits from TextColor
* Call `Render()` after changing icon color

**Q: Calendar dropdown is too narrow**

* Increase control `Width` property
* For week numbers, use minimum 280px width
* Dropdown auto-sizes to match control width

***

### Related Resources

* [**KT Color Utility**](https://www.kimtoo.net/sdk/utilities/kt-color) - Advanced color management and theming
* [**KT Brush Utility**](https://www.kimtoo.net/sdk/utilities/kt-brush) - Gradient and pattern rendering

***
