---
description: Human-Centered Color System for .NET
cover:
  light: ../.gitbook/assets/colors_light.png
  dark: ../.gitbook/assets/colors_dark.png
coverY: 0
layout:
  width: default
  cover:
    visible: true
    size: full
  title:
    visible: false
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

# 🔹 Kt-Color

## <mark style="color:$primary;">**The only alternative to System.Drawing.Color built on actual color theory**</mark>

_Because color management shouldn't require a PhD in color theory_

***

### Overview

KtColor is a complete color management system for .NET WinForms that replaces the limitations of `System.Drawing.Color` with a developer-friendly API built on HSL color theory, variable theming, and intuitive syntax.

#### Why KtColor Exists

`System.Drawing.Color` was designed for basic color representation, not modern UI development:

* **No color theory support** - RGB values don't map to how humans perceive color
* **No theme system** - Can't define semantic colors like "Primary" or "Success"
* **No shade generation** - Manual calculation of lighter/darker variants
* **Poor string parsing** - Limited format support
* **No opacity management** - Alpha channels are awkward to work with

KtColor solves these problems with a unified system built for human perception and modern theming.

***

### Core Concepts

#### 1. Color Representation

KtColor uses **HSL (Hue, Saturation, Lightness)** internally because it matches human color perception:

```csharp
// Access HSL properties
var color = KtColor.Blue;
float hue = color.Hue;           // 0-360°
float saturation = color.Saturation; // 0-1
float lightness = color.Lightness;   // 0-1
int shade = color.Shade;         // 0-100%
```

#### 2. Three Color Types

**Native Colors** - Predefined palette colors with names:

```csharp
KtColor.Blue      // @Blue
KtColor.Slate     // @Slate
KtColor.PRIMARY   // $Primary (variable)
```

**Custom Colors** - From hex, RGB, or System.Drawing.Color:

```csharp
KtColor custom = "#FF5733";
KtColor custom = Color.FromArgb(255, 87, 51);
```

**Empty/Transparent**:

```csharp
KtColor.Empty        // No color
KtColor.Transparent  // Transparent color
```

***

### Palette System

#### Base Colors (Neutrals)

```csharp
KtColor.Slate   // #64748B - Cool gray
KtColor.Gray    // #6B7280 - Neutral gray
KtColor.Zinc    // #71717A - Warm gray
KtColor.Stone   // #78716C - Earth gray
```

#### Accent Colors (Main Palette)

```csharp
// Cool colors
KtColor.Blue, Sky, Cyan, Teal, Emerald, Green

// Warm colors
KtColor.Red, Rose, Pink, Fuchsia, Purple, Violet, Indigo

// Yellow spectrum
KtColor.Lime, Yellow, Amber, Orange
```

#### Theme Variables

```csharp
KtColor.PRIMARY    // $Primary - Main brand color
KtColor.SECONDARY  // $Secondary - Secondary brand
KtColor.ACCENT     // $Accent - Highlight color
KtColor.NEUTRAL    // $Neutral - Neutral UI elements

KtColor.BASE       // $Base - Background (alias for BASE_2)
KtColor.BASE_1     // $Base_1 - Lightest background
KtColor.BASE_2     // $Base_2 - Default background
KtColor.BASE_3     // $Base_3 - Darkest background
KtColor.CONTENT    // $Content - Text/content color

// Status colors
KtColor.SUCCESS    // $Success - Success states
KtColor.INFO       // $Info - Information
KtColor.WARNING    // $Warning - Warnings
KtColor.ERROR      // $Error - Errors
```

***

### Shade System

Every palette color includes 11 shades (0-100 in 10% increments):

```csharp
// Indexer syntax - percentage (0-100)
KtColor.Blue[0]    // Darkest (almost black)
KtColor.Blue[50]   // Middle (base color)
KtColor.Blue[100]  // Lightest (almost white)

// Indexer syntax - float (0.0-1.0)
KtColor.Blue[0f]    // Darkest
KtColor.Blue[0.5f]  // Middle
KtColor.Blue[1f]    // Lightest

// Operators for adjustment
var darker = KtColor.Blue - 10;   // -10% lightness
var lighter = KtColor.Blue + 20;  // +20% lightness
```

***

### String Format Support

#### Parsing Formats

```csharp
// Palette colors
KtColor.Parse("Blue")           // Base color
KtColor.Parse("@Blue")          // Explicit palette
KtColor.Parse("$Primary")       // Variable

// With shades
KtColor.Parse("Blue[50]")       // 50% lightness
KtColor.Parse("@Slate[30]")     // 30% lightness

// With opacity
KtColor.Parse("Blue%50")        // 50% opacity
KtColor.Parse("Blue[70]%80")    // 70% lightness, 80% opacity

// Hex colors
KtColor.Parse("#FF5733")        // RGB hex
KtColor.Parse("#FF5733%50")     // With opacity

// CSS formats
KtColor.Parse("rgb(255,87,51)")
KtColor.Parse("rgba(255,87,51,0.5)")
KtColor.Parse("hsl(9,100%,60%)")
KtColor.Parse("hsla(9,100%,60%,0.5)")
```

#### Rendering Formats

```csharp
var color = KtColor.Blue[60]%80;

// String representation
color.ToString()      // "Blue[60]%80"
color.Name           // "@Blue" (for palette colors)

// Web formats
color.Web()          // "#3B82F6" or color name
color.Hex()          // "#3B82F6"
color.RGB()          // "rgb(59,130,246)"
color.HSL()          // "hsl(217,91.2%,59.8%)"

// With opacity
color.RGB(web: true) // "rgba(59,130,246,0.80)"
color.HSL()          // "hsla(217,91.2%,59.8%,0.80)"

// Internal representation
color.Int()          // ARGB as int32
color.Render()       // System.Drawing.Color
```

***

### Operators Reference

#### Implicit Conversions

```csharp
// From string
KtColor color = "Blue";
KtColor color = "#FF5733";

// From System.Drawing.Color
KtColor color = Color.Red;

// From ARGB int
KtColor color = 0xFF0000FF;

// To System.Drawing.Color
Color systemColor = KtColor.Blue;

// To string
string str = KtColor.Blue;  // "Blue"
```

#### Lightness Operations

```csharp
// Increment/decrement (10% steps)
var lighter = color + 1;   // +10% lightness
var darker = color - 1;    // -10% lightness
var lighter = ++color;     // Prefix: +10%
var darker = --color;      // Prefix: -10%

// By amount (percentage)
var lighter = color + 25;  // +25% lightness
var darker = color - 15;   // -15% lightness

// By float (0.0-1.0)
var lighter = color + 0.25f;  // +25% lightness
var darker = color - 0.15f;   // -15% lightness
```

#### Opacity Operations

```csharp
// Set opacity (modulo operator)
var transparent = color % 50;   // 50% opacity
var opaque = 100 % color;       // 100% opacity (either order)

// Divide opacity
var half = color / 2;          // Half opacity
```

#### Color Inversion

```csharp
// Invert lightness
var inverted = !color;

// For theme variables: returns content color
var content = !KtColor.PRIMARY;  // Returns PRIMARY's content color

// Auto-contrast adjustment (subtle)
var adjusted = ~color;  // Adjusts by ±7% for readability
```

#### Conditional Operations

```csharp
// Boolean coalescing
var active = userColor | KtColor.PRIMARY;  // Use userColor or fall back

// Condition-based inversion
var result = true & color;   // Returns color if true
var result = false & color;  // Returns inverted if false
var result = true | color;   // Returns inverted if true
var result = false | color;  // Returns color if false
```

#### Color Mixing

```csharp
// Combine colors (alpha blending)
var mixed = color1 + color2;

// Subtract colors
var diff = color1 - color2;

// Mix with percentage
var blend = KtColor.Mix(color1, color2, 30f);  // 30% color2, 70% color1
```

#### Comparison

```csharp
// Lightness comparison
bool isDarker = color1 < color2;
bool isLighter = color1 > color2;

// Equality
bool same = color1 == color2;
bool different = color1 != color2;
```

#### Boolean Context

```csharp
// Check if color has value (not empty/transparent)
if (color)  // true if not Empty and not None
{
    // Color is valid
}
```

***

### Property Inspection

#### Color Properties

```csharp
// RGB components
int r = color.R;  // 0-255
int g = color.G;  // 0-255
int b = color.B;  // 0-255
int a = color.A;  // 0-255

// HSL components
float hue = color.Hue;           // 0-360
float saturation = color.Saturation;  // 0-1
float lightness = color.Lightness;    // 0-1
int shade = color.Shade;         // 0-100
int opacity = color.Opacity;     // 0-100

// Base color
Color baseColor = color.Base;    // Underlying System.Drawing.Color
object baseValue = color.@base;  // String (palette) or Color (custom)
```

#### State Checks

```csharp
// Emptiness
bool isEmpty = color.IsEmpty;         // Color.Empty
bool isTransparent = color.IsTransparent;  // Color.Transparent
bool isClear = color.IsClear;         // Empty or fully transparent
bool hasValue = color.Any;            // Has a value

// Opacity
bool isOpaque = color.IsOpaque;       // 100% opacity
bool isTranslucent = color.IsTranslucent;  // Partial opacity

// Type checks
bool isNative = color.IsNative;       // Palette color
bool isCustom = color.IsCustom;       // Custom RGB color
bool isVariable = color.IsVariable;   // Theme variable ($)
bool isTheme = color.IsTheme;         // Root theme variable
bool isRoot = color.IsRoot;           // No shade applied
bool isNamed = color.IsNamed;         // Has a name
bool isKnownColor = color.IsKnownColor;  // System.Drawing.KnownColor
```

***

### Theme System

#### Setting Theme Variables

```csharp
// Set individual variables
KtColor.@default("Primary", Color.FromArgb(96, 93, 255));
KtColor.@default("Base_1", Color.FromArgb(50, 57, 74));

// Apply light/dark theme presets
KtColor.Render(isDark: true);   // Dark mode
KtColor.Render(isDark: false);  // Light mode
KtColor.Render(isDark: null);   // Keep current

// Check current theme
bool isDarkMode = KtColor.IsDark();   // BASE < !BASE
bool isLightMode = KtColor.IsLight(); // BASE > !BASE
```

#### Theme Change Events

```csharp
// Subscribe to theme changes
KtColor.ThemeChanged += (isDark) => 
{
    // Respond to theme change
    RefreshUI();
};

// Subscribe to variable changes
KtColor.VariableChanged += (sender, e) => 
{
    string variableName = e.PropertyName;  // "Primary", "Base_1", etc.
    // Respond to specific variable change
};
```

#### Default Theme Colors

**Dark Mode (default)**:

```csharp
Content: #F5F5F5 (WhiteSmoke)
Base_1:  #32394A (Light surface)
Base_2:  #1B2336 (Default surface)
Base_3:  #0F172B (Dark surface)
Neutral: #515765 (Gray)
```

**Light Mode**:

```csharp
Content: #1B2336 (Dark text)
Base_1:  #FFFFFF (White)
Base_2:  #F8FAFG (Off-white)
Base_3:  #E8EBEE (Light gray)
Neutral: #F5F5F5 (WhiteSmoke)
```

***

### Advanced Features

#### Content Color Calculation

Automatic foreground color for any background:

```csharp
var background = KtColor.Blue[30];
var foreground = !background;  // High contrast text color
var foreground = background.Invert();  // Same as above
var foreground = background.Content();  // For theme variables
```

#### Opaque Color Blending

Flatten translucent colors onto a background:

```csharp
var translucent = KtColor.Blue % 50;  // 50% opacity
var background = KtColor.White;
var opaque = translucent.Opaque(background);  // Flattened result
```

#### Color Iteration

Enumerate all shades:

```csharp
foreach (var shade in KtColor.Blue)
{
    // Iterates 0%, 10%, 20%, ... 100%
    DrawSwatch(shade);
}
```

#### Random Colors

```csharp
var random = KtColor.Random();      // Random palette color
var randomDark = KtColor.Random(30);  // Random at 30% lightness
```



### Design Decisions

#### Why HSL over RGB?

**Human perception** - HSL maps to how humans naturally think about color:

* "Make it lighter" → Increase L
* "More vibrant" → Increase S
* "Change the color" → Adjust H

RGB requires mental math to achieve these effects. With RGB, making a color "lighter" means adding white to all channels proportionally, which is unintuitive.

**Predictable shades** - In HSL, generating a lighter shade is trivial:

```csharp
// HSL - Simple and predictable
var lighter = color[70];  // 70% lightness

// RGB - Complex calculation required
var lighter = Color.FromArgb(
    (int)(color.R + (255 - color.R) * 0.3),
    (int)(color.G + (255 - color.G) * 0.3),
    (int)(color.B + (255 - color.B) * 0.3)
);
```

**Consistent brightness** - All colors at the same L value have perceptually similar brightness, making UI consistency easier.

#### Why String-Based Palette Names?

Using strings (`"Blue"`) instead of enums provides:

1. **Extensibility** - Add custom colors without recompiling
2. **Serialization** - Natural JSON/config file support
3. **Dynamic theming** - Runtime color palette switching
4. **Designer support** - PropertyGrid string editor works out of the box

The trade-off is type safety, mitigated by:

* `TryParse` for validation
* Static properties for common colors (`KtColor.Blue`)
* IntelliSense support through static members

#### Why Variable System?

Theme variables (`$Primary`, `$Base`) solve a fundamental problem in UI development: **semantic colors**.

Traditional approach:

```csharp
// Hard-coded colors throughout application
button.BackColor = Color.FromArgb(96, 93, 255);
label.ForeColor = Color.FromArgb(96, 93, 255);
panel.BackColor = Color.FromArgb(27, 35, 54);
```

Problems:

* Can't change brand colors without find-replace
* No dark mode support
* Inconsistent colors across components
* Can't theme at runtime

KtColor approach:

```csharp
// Semantic colors
button.BackColor = KtColor.PRIMARY;
label.ForeColor = KtColor.PRIMARY;
panel.BackColor = KtColor.BASE;

// One-line theme change
KtColor.Render(isDark: true);  // Everything updates
```

#### Why Operator Overloading?

Operators make color manipulation read like natural language:

```csharp
// Traditional
var hover = ColorHelper.Lighten(baseColor, 0.1f);
var disabled = ColorHelper.SetOpacity(baseColor, 0.4f);
var contrast = ColorHelper.GetContrast(background);

// KtColor
var hover = baseColor + 10;
var disabled = baseColor % 40;
var contrast = !background;
```

The code becomes self-documenting. `color + 10` obviously means "lighter", `color % 50` clearly indicates opacity.

***

### Performance Considerations

#### Lazy Evaluation

KtColor uses lazy property evaluation to minimize allocations:

```csharp
// Properties calculated on first access
public float Hue => _hue ??= Base.GetHue();
public Color Base => _base ??= CalculateBase();
```

Once calculated, values are cached. This means:

* Creating `KtColor.Blue` is cheap (no calculations)
* First `.Render()` call performs HSL→RGB conversion
* Subsequent renders use cached value

#### Theme Variable Invalidation

When theme variables change, cached values are invalidated via hash code:

```csharp
if (prevHashCode != _hashcode && IsVariable)
{
    _base = _value = null;  // Invalidate cache
    _hue = _saturation = _lightness = null;
    prevHashCode = _hashcode;
}
```

This ensures theme changes propagate while maintaining performance during normal operation.

#### Allocation Patterns

```csharp
// No allocation - returns cached instance
var color = KtColor.Blue;

// Small allocation - new KtColor instance
var shade = KtColor.Blue[50];

// Allocation on render
Color gdi = shade.Render();  // Creates System.Drawing.Color
```

Best practice: Store KtColor in properties, render only when needed for painting.

***

### Integration Patterns

#### PropertyGrid Support

Full designer integration via `TypeConverter`:

```csharp
[TypeConverter(typeof(KtColorConverter))]
public class MyControl : Control
{
    public KtColor BackgroundColor { get; set; } = KtColor.PRIMARY;
}
```

The PropertyGrid shows:

* Dropdown with standard values
* String editor for custom values
* Color picker for RGB colors
* Live preview of the color

#### Custom Editor

KtColor includes a custom color editor that extends the standard .NET color picker:

```csharp
#if NET
[Editor("System.Drawing.Design.ColorEditor...", 
        "System.Drawing.Design.UITypeEditor...")]
#else
[Editor(typeof(KtColorEditor), typeof(UITypeEditor))]
#endif
```

Features:

* Palette color browser
* Shade selector
* Opacity control
* Search functionality
* Theme variable access

#### JSON Serialization

Implicit JToken conversion for JSON.NET:

```csharp
var json = new JObject
{
    ["primary"] = KtColor.PRIMARY,
    ["background"] = KtColor.BASE[20]
};

// Output:
// { 
//   "primary": "#605DFF",
//   "background": "#1B2336"
// }
```

Deserialize back:

```csharp
KtColor primary = json["primary"].ToString();
KtColor background = json["background"].ToString();
```

***

### Migration Guide

#### From System.Drawing.Color

```csharp
// Before
Color btnColor = Color.Blue;
Color btnHover = ControlPaint.Light(btnColor);
Color btnDisabled = Color.FromArgb(102, btnColor);

// After
KtColor btnColor = KtColor.Blue;
KtColor btnHover = btnColor + 10;
KtColor btnDisabled = btnColor % 40;
```

#### From String Color Names

```csharp
// Before
public string BackgroundColor { get; set; } = "Blue";
// ... manual parsing in OnPaint

// After
public KtColor BackgroundColor { get; set; } = KtColor.Blue;
// Render() returns System.Drawing.Color directly
```

#### Adding Theme Support

```csharp
// Before - hard-coded colors
public class MyButton : Button
{
    public MyButton()
    {
        BackColor = Color.FromArgb(96, 93, 255);
        ForeColor = Color.White;
    }
}

// After - theme-aware
public class MyButton : Button
{
    public MyButton()
    {
        BackColor = KtColor.PRIMARY;
        ForeColor = KtColor.CONTENT;
    }
    
    protected override void OnPaint(PaintEventArgs e)
    {
        e.Graphics.FillRectangle(
            new SolidBrush(BackColor),  // Auto-converts KtColor→Color
            ClientRectangle
        );
    }
}

// Theme change applies automatically
KtColor.Render(isDark: true);
```

***

### Best Practices

#### 1. Use Theme Variables for Semantic Colors

```csharp
// Good - semantic meaning
button.BackColor = KtColor.PRIMARY;
errorLabel.ForeColor = KtColor.ERROR;

// Avoid - loses semantic meaning
button.BackColor = KtColor.Blue;
errorLabel.ForeColor = KtColor.Red;
```

#### 2. Store KtColor, Render Late

```csharp
// Good - single source of truth
private KtColor _buttonColor = KtColor.PRIMARY;

protected override void OnPaint(PaintEventArgs e)
{
    using var brush = new SolidBrush(_buttonColor.Render());
    e.Graphics.FillRectangle(brush, bounds);
}

// Avoid - loses shade/opacity information
private Color _buttonColor = KtColor.PRIMARY.Render();
```

#### 3. Use Operators for Variations

```csharp
// Good - clear intent
var hover = normalColor + 10;
var pressed = normalColor - 10;
var disabled = normalColor % 40;

// Avoid - obscures relationship
var hover = KtColor.Parse("Blue[60]");
var pressed = KtColor.Parse("Blue[40]");
var disabled = KtColor.Parse("Blue%40");
```

#### 4. Leverage Content Colors

```csharp
// Good - automatic contrast
var bgColor = KtColor.PRIMARY;
var textColor = !bgColor;  // High contrast text

// Avoid - manual contrast calculation
var bgColor = KtColor.PRIMARY;
var textColor = bgColor.Lightness > 0.5 ? KtColor.Black : KtColor.White;
```

#### 5. Subscribe to Theme Changes

```csharp
public class ThemedControl : Control
{
    public ThemedControl()
    {
        KtColor.ThemeChanged += OnThemeChanged;
        UpdateColors();
    }
    
    private void OnThemeChanged(bool? isDark)
    {
        UpdateColors();
        Invalidate();
    }
    
    protected override void Dispose(bool disposing)
    {
        if (disposing)
            KtColor.ThemeChanged -= OnThemeChanged;
        base.Dispose(disposing);
    }
}
```

***

### Common Pitfalls

#### 1. Comparing Rendered Colors

```csharp
// Wrong - compares System.Drawing.Color instances
if (color1.Render() == color2.Render()) { }

// Right - compares KtColor semantics
if (color1 == color2) { }
```

#### 2. Losing Shade Information

```csharp
// Wrong - loses shade
Color temp = KtColor.Blue[30];
KtColor result = temp;  // Now Blue[50] (root)

// Right - keep as KtColor
KtColor result = KtColor.Blue[30];
```

#### 3. Not Handling Empty Colors

```csharp
// Wrong - potential null reference
var rendered = color.Render();
e.Graphics.FillRectangle(new SolidBrush(rendered), bounds);

// Right - check first
if (color)  // or: if (!color.IsEmpty)
{
    using var brush = new SolidBrush(color.Render());
    e.Graphics.FillRectangle(brush, bounds);
}
```

#### 4. Ignoring Opacity in Rendering

```csharp
// Wrong - opacity lost if background not specified
var translucent = KtColor.Blue % 50;
var final = translucent.Render();  // Still has alpha channel

// Right - flatten to opaque if needed
var translucent = KtColor.Blue % 50;
var final = translucent.Opaque(backgroundColor);
```

***

### API Summary

#### Static Properties

* 22 palette colors: `Slate`, `Blue`, `Red`, etc.
* 11 theme variables: `PRIMARY`, `BASE`, `CONTENT`, etc.
* Special: `Empty`, `Transparent`, `White`, `Black`

#### Instance Properties

* RGB: `R`, `G`, `B`, `A`
* HSL: `Hue`, `Saturation`, `Lightness`, `Shade`
* State: `IsEmpty`, `IsOpaque`, `IsNative`, `IsVariable`
* Meta: `Name`, `Base`, `Opacity`

#### Static Methods

* `Parse(string)` - Parse any color format
* `TryParse(string, out KtColor)` - Safe parsing
* `Render(bool? isDark)` - Set theme
* `@default(string, Color)` - Set variable
* `Mix(c1, c2, percentage)` - Blend colors
* `Random(shade?)` - Random color

#### Instance Methods

* `Render()` - Convert to System.Drawing.Color
* `ToString()` - KtColor string representation
* `Hex()`, `RGB()`, `HSL()`, `Web()` - Format conversion
* `Invert()`, `Content()`, `Mirror()` - Color transforms
* `Opaque(background)` - Flatten alpha

#### Operators

* `+`, `-` - Adjust lightness
* `%` - Set opacity
* `/` - Divide opacity
* `!` - Invert
* `~` - Auto-contrast
* `|` - Coalesce
* `==`, `!=`, `<`, `>` - Compare

***

_KtColor - Because color management shouldn't require a PhD in color theory_
