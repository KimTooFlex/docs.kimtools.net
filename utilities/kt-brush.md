---
description: Modern Brush System for WinForms
---

# 🔹 Kt-Brush

### <mark style="color:$primary;">The Problem with Traditional WinForms UI</mark>

Let's be honest: **WinForms wasn't built for modern UI design.**

In 2025, users expect applications that rival web experiences—smooth gradients, dynamic color schemes, and fluid visual transitions. Yet WinForms developers are stuck with the same limited brush system from the early 2000s:

#### What's Wrong with Standard WinForms Brushes?

**Limited Gradient Support**

* Creating gradients requires manual `LinearGradientBrush` instantiation for every control
* No declarative way to define gradients in the designer
* Angle adjustments mean rewriting entire brush initialization code
* Rectangle dependency makes gradients rigid and hard to reuse

**Poor Developer Experience**

* Brushes aren't property-bindable in a meaningful way
* No type conversion support for seamless string/color conversions
* Zero support for empty/transparent state checking
* Manual cleanup and disposal required everywhere

**Design-Time Nightmare**

* Properties don't refresh properly when changed
* No visual feedback in the designer
* Can't serialize complex brush configurations
* TypeConverter support is either missing or broken

**No Modern Patterns**

* No fluent API for brush manipulation
* Can't chain operations or create brush variations
* No implicit conversions between Color and Brush types
* Impossible to create reusable brush presets

#### The Real Cost

These limitations force developers to choose between:

1. **Beautiful UI** - Write hundreds of lines of boilerplate brush management code
2. **Fast Development** - Ship applications that look dated and unprofessional

Modern client applications demand visual sophistication. When your competition is delivering Electron apps with CSS gradients and your desktop app looks like it's from Windows XP, you've already lost.

***

### Introducing KtBrush

**KtBrush** is a complete reimagining of the WinForms brush system, designed for modern UI development with developer experience as a first-class concern.

#### Core Philosophy

1. **Declarative First** - Define what you want, not how to build it
2. **Type-Safe Everything** - Leverage C# features for compile-time safety
3. **Designer-Friendly** - Full PropertyGrid integration with live updates
4. **Zero Boilerplate** - Implicit conversions eliminate repetitive code

***

### Key Features

#### 🎨 Unified Brush Abstraction

Three brush types, one elegant interface:

```csharp
// None - For transparent/no-fill scenarios
KtBrush.None

// Solid - Single color with full KtColor support
KtBrush.Solid

// Gradient - Multi-color with angle control
KtBrush.Gradient
```

#### 🔄 Automatic Type Conversions

Stop writing conversion code. KtBrush handles it:

```csharp
// Color to Brush - Just works
KtBrush brush = Color.Blue;

// KtColor to Brush - Seamless
KtBrush brush = new KtColor(255, 0, 0);

// Tuple to Gradient - Intuitive
KtBrush gradient = (KtColor.Blue, KtColor.Red);

// Array to Gradient - Natural
KtBrush gradient = new[] { Color.Blue, Color.Red };
```

#### ⚡ Fluent Gradient Operations

Manipulate gradients like you manipulate data:

```csharp
// Set angle with % operator
var brush = gradient % 45;

// Rotate gradients
var rotated = brush + 90;  // Clockwise
var counter = brush - 45;  // Counter-clockwise

// Chain operations
var final = gradient % 0 + 180;
```

#### 🔍 Smart State Detection

Built-in checks for common scenarios:

```csharp
if (brush.IsEmpty) { /* ... */ }
if (brush.IsTransparent) { /* ... */ }

// Use as boolean
if (brush) { /* brush is not None and not empty */ }

// Coalescing operator support
var activeBrush = userBrush | defaultBrush;
```

#### 🎯 Designer Integration

Full PropertyGrid support with proper refresh behavior:

* **NotifyParentProperty** - Parent controls update automatically
* **RefreshProperties** - Triggers repaints when needed
* **Type Conversion** - String input works seamlessly
* **Expandable Properties** - Gradient properties expand in place

#### 📐 Render Anywhere

Single API for multiple rendering targets:

```csharp
// String representation
string css = brush.Render();
// Output: "gradient(45,#0000FF,#FF0000)"

// GDI+ Brush with rectangle context
Brush gdiBrush = brush.Render(controlBounds);
// Returns: LinearGradientBrush or SolidBrush
```

#### 🎁 Bonus: Squircle Support

Modern rounded rectangles with a single method:

```csharp
var path = KtBrush.Squircle(bounds, radiusPercent);
// Smooth, iOS-style rounded corners
```

***

### Real-World Examples

#### Before: Traditional WinForms

```csharp
public class MyControl : Control
{
    private Color _startColor = Color.Blue;
    private Color _endColor = Color.Red;
    private int _angle = 45;

    protected override void OnPaint(PaintEventArgs e)
    {
        if (_startColor.A == 0 && _endColor.A == 0)
            return; // Handle transparent case

        Brush brush;
        if (_startColor == _endColor)
        {
            brush = new SolidBrush(_startColor);
        }
        else
        {
            brush = new LinearGradientBrush(
                this.ClientRectangle,
                _startColor,
                _endColor,
                _angle
            );
        }

        try
        {
            e.Graphics.FillRectangle(brush, this.ClientRectangle);
        }
        finally
        {
            brush.Dispose();
        }
    }

    // Plus separate properties for StartColor, EndColor, Angle...
    // Plus designer serialization code...
    // Plus type conversion code...
}
```

#### After: With KtBrush

```csharp
public class MyControl : Control
{
    [Category("Appearance")]
    public KtBrush Background { get; set; } = 
        (KtColor.Blue, KtColor.Red) % 45;

    protected override void OnPaint(PaintEventArgs e)
    {
        if (!Background) return;

        using var brush = Background.Render(ClientRectangle);
        e.Graphics.FillRectangle(brush, ClientRectangle);
    }
}
```

**90% less code. 100% more maintainable.**

***

### Advanced Patterns

#### Conditional Brushes

```csharp
// Use coalescing for fallbacks
var effectiveBrush = customBrush | themeBrush | KtBrush.Solid;

// Boolean checks
if (highlightBrush)
    DrawHighlight(highlightBrush);
```

#### Dynamic Gradient Rotation

```csharp
// Animate gradient rotation
private void Timer_Tick(object sender, EventArgs e)
{
    Background = Background + 5; // Rotate 5° per tick
    Invalidate();
}
```

#### Serialization-Ready

```csharp
// Renders to string for persistence
string saved = brush.Render();
// "gradient(90,#FF0000,#0000FF)"

// Parse back from string
var restored = KtBrush.Parse(saved);
```

#### JSON Integration

```csharp
// Implicit JToken conversion
JToken json = brush;
// Solid: ["#FF0000"]
// Gradient: ["#FF0000", "#0000FF"]
```

***

### Technical Highlights

#### Architecture

* **Abstract Base Class** - `KtBrush` provides common interface
* **Sealed Implementations** - `KtBrushNone`, `KtBrushSolid`, `KtBrushGradient`
* **Property Change Notifications** - Full `INotifyPropertyChanged` support
* **Implicit Operators** - Seamless type conversions

#### Type Safety

* No magic strings
* Compile-time type checking
* Null-safe throughout
* Explicit empty state handling

#### Performance

* Lazy rendering - brushes created only when needed
* Minimal allocations
* Efficient equality checks
* No reflection in hot paths

***

### Getting Started

#### Basic Usage

```csharp
using KimTools.WinForms;

// In your control
public KtBrush ButtonBrush { get; set; } = Color.Blue;

// In paint method
using var brush = ButtonBrush.Render(bounds);
e.Graphics.FillRectangle(brush, bounds);
```

#### Creating Gradients

```csharp
// Method 1: Direct instantiation
var gradient = new KtBrushGradient(
    KtColor.Parse("#FF6B6B"),
    KtColor.Parse("#4ECDC4"),
    angle: 135
);

// Method 2: Implicit conversion
KtBrush gradient = (Color.Red, Color.Blue);

// Method 3: Fluent API
var gradient = KtBrush.Gradient % 45;
gradient.StartColor = "#FF6B6B";
gradient.StopColor = "#4ECDC4";
```

***

***

### The Bottom Line

**WinForms doesn't have to look dated.**

KtBrush brings modern UI capabilities to the platform you already know, without forcing you to rewrite your application in WPF, Avalonia, or Electron.

Stop fighting your UI framework. Start shipping beautiful applications.

***

***

_Built with ❤️ for the Legacy WinForms community_
