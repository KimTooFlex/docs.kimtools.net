---
icon: window-flip
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

# Window

KtWindow is a modern, feature-rich window/form component for WinForms that brings beautiful dark mode support, gradient backgrounds, and flicker-free rendering to your applications. Built with native Windows API optimizations for professional, smooth user experiences.

***

### 🌟 Cool Features

#### ✨ Automatic Dark Mode

Native Windows 10/11 title bar dark mode that automatically matches your theme.

```csharp
public partial class MyWindow : KtWindow
{
    public MyWindow()
    {
        InitializeComponent();
        // Dark mode automatically applied based on KtColor.IsDark()
    }
}
```

**How it works:**

* Automatically detects system theme or your custom theme
* Updates title bar to match (dark or light)
* No flickering during theme transitions
* Native Windows 10/11 immersive dark mode API

***

#### 🎨 Gradient Backgrounds

Beautiful gradient backgrounds with zero code complexity.

```csharp
// Set gradient background in Designer or code
this.Background = new KtBrushGradient(KtColor.PRIMARY, KtColor.ACCENT);

// Or use angle for direction
var gradient = new KtBrushGradient(KtColor.PRIMARY, KtColor.ACCENT)
{
    Angle = 45 // Diagonal gradient
};
this.Background = gradient;
```

**Features:**

* Smooth gradients with any two colors
* Adjustable angle for direction
* Automatic theme updates
* Flicker-free rendering

***

#### 🚀 Zero Flicker Rendering

Optimized with native Windows API for butter-smooth rendering.

```csharp
public KtWindow()
{
    InitializeComponent();
    // Double buffering automatically enabled
    // Native API optimizations applied
    // No flickering during resize or theme changes
}
```

**What makes it flicker-free:**

* Native `WS_EX_COMPOSITED` style for hardware acceleration
* Double buffering enabled by default
* Optimized paint events
* Smart invalidation (only redraws what changed)

***

#### 🔄 Auto Theme Synchronization

Automatically updates when theme changes - no manual refresh needed!

```csharp
public MyWindow()
{
    InitializeComponent();
    // Window automatically subscribes to theme changes
    // Updates background, foreground, and title bar automatically
}
```

**Automatic updates when:**

* User switches between dark/light mode
* Theme colors change
* System theme changes

***

#### 💪 Drop Shadow Support

Beautiful drop shadow for borderless windows.

```csharp
// For borderless windows
this.FormBorderStyle = FormBorderStyle.None;

// Shadow automatically applied via DWM API
// Creates modern, floating window effect
```

***

#### 🎯 Smart Window Management

Intelligent features that just work.

```csharp
// Dynamic title updates
this.Title("My Application - Loading...");
string currentTitle = this.Title(); // Get current title

// Smart foreground color detection
var foreColor = this.GetForeground();
// Returns Foreground property or falls back to this.ForeColor

// Take snapshots
Image snapshot = this.Snapshot();
```

***

#### Creating a KtWindow

**Step 1: Inherit from KtWindow**

```csharp
using KimTools.WinForms;

namespace MyApp.Forms
{
    public partial class MainWindow : KtWindow
    {
        public MainWindow()
        {
            InitializeComponent();
        }
    }
}
```

**Step 2: Set Background (Optional)**

```csharp
public MainWindow()
{
    InitializeComponent();
    
    // Solid background
    this.Background = KtColor.BASE;
    
    // Or gradient background
    this.Background = new KtBrushGradient(
        KtColor.PRIMARY, 
        KtColor.ACCENT
    );
}
```

**Step 3: Set Foreground (Optional)**

```csharp
public MainWindow()
{
    InitializeComponent();
    
    this.Foreground = KtColor.CONTENT;
    // Automatically applies to text and controls
}
```

That's it! You now have a modern window with dark mode support.

***

### Properties

#### Background

Sets the window background (solid color or gradient).

```csharp
[Category(" 🗲 KimTools")]
public KtBrush Background { get; set; }
```

**Examples:**

```csharp
// Solid color
this.Background = KtColor.BASE;
this.Background = new KtBrushSolid(Color.Navy);

// Gradient (horizontal by default)
this.Background = new KtBrushGradient(
    KtColor.PRIMARY, 
    KtColor.ACCENT
);

// Gradient with angle
var gradient = new KtBrushGradient(KtColor.PRIMARY, KtColor.ACCENT);
gradient.Angle = 90; // Vertical
this.Background = gradient;

// Transparent (shows default)
this.Background = KtBrush.None;
```

***

#### Foreground

Sets the window foreground color (text and UI elements).

```csharp
[Category(" 🗲 KimTools")]
public KtColor Foreground { get; set; }
```

**Examples:**

```csharp
// Theme color
this.Foreground = KtColor.CONTENT;

// Custom color
this.Foreground = new KtColor(Color.White);

// Inverted color
this.Foreground = !KtColor.NEUTRAL;

// Empty (uses default)
this.Foreground = KtColor.Empty;
```

***

#### Text (Title)

Gets or sets the window title.

```csharp
[Category(" 🗲 KimTools")]
public override string Text { get; set; }
```

**Examples:**

```csharp
// Set title
this.Text = "My Application";

// Or use Title() method
this.Title("My Application");
```

***

#### IsDark / IsLight (Read-Only)

Detects current theme mode.

```csharp
[Browsable(false)]
public bool IsDark { get; }

[Browsable(false)]
public bool IsLight { get; }
```

**Examples:**

```csharp
if (this.IsDark)
{
    // Do something for dark mode
    icon.Image = darkModeIcon;
}

if (this.IsLight)
{
    // Do something for light mode
    icon.Image = lightModeIcon;
}
```

***

### Background & Foreground

#### Setting Background Colors

**Solid Colors:**

```csharp
// Using KtColor theme colors
this.Background = KtColor.BASE;      // Main background
this.Background = KtColor.BASE_2;    // Elevated background
this.Background = KtColor.PRIMARY;   // Primary theme color

// Using standard colors
this.Background = new KtBrushSolid(Color.Navy);
this.Background = new KtBrushSolid(Color.FromArgb(25, 30, 36));
```

**Gradient Colors:**

```csharp
// Simple gradient (left to right)
this.Background = new KtBrushGradient(
    KtColor.PRIMARY,
    KtColor.ACCENT
);

// Gradient with custom angle
var gradient = new KtBrushGradient(
    startColor: KtColor.PRIMARY,
    stopColor: KtColor.ACCENT
);
gradient.Angle = 45;  // Diagonal
this.Background = gradient;

// Vertical gradient (top to bottom)
var verticalGradient = new KtBrushGradient(
    KtColor.PRIMARY,
    KtColor.ACCENT
);
verticalGradient.Angle = 90;
this.Background = verticalGradient;

// Gradient with opacity
var gradientWithOpacity = new KtBrushGradient(
    new KtColor("$Primary", null, 50),  // 50% opacity
    new KtColor("$Accent", null, 50)
);
this.Background = gradientWithOpacity;
```

***

#### Setting Foreground Colors

```csharp
// Theme colors
this.Foreground = KtColor.CONTENT;   // Default content color
this.Foreground = KtColor.PRIMARY;   // Primary theme color

// Custom colors
this.Foreground = new KtColor(Color.White);
this.Foreground = new KtColor("#FFFFFF");

// Inverted colors
this.Foreground = !KtColor.BASE;     // Inverts base color

// Dynamic based on background
if (this.IsDark)
    this.Foreground = KtColor.White;
else
    this.Foreground = KtColor.Black;
```

***

### Dark Mode

#### Automatic Dark Mode

KtWindow automatically applies native dark mode to the title bar.

```csharp
public MainWindow()
{
    InitializeComponent();
    
    // Dark mode automatically enabled when KtColor.IsDark() is true
    // Title bar updates automatically
    // No code needed!
}
```

**How it detects dark mode:**

1. Checks `KtColor.IsDark()` - your theme setting
2. Applies Windows 10/11 immersive dark mode API
3. Updates title bar color automatically
4. Syncs with theme changes

***

#### Manual Dark Mode Control

```csharp
// Force render mode update
this.RenderMode();

// Check current mode
if (this.IsDark)
{
    // Update dark mode specific UI
}

// Render updates everything
this.Render();
```

***

#### Borderless Window Shadow

For modern borderless windows, KtWindow automatically adds a drop shadow:

```csharp
public MainWindow()
{
    InitializeComponent();
    
    // Set borderless
    this.FormBorderStyle = FormBorderStyle.None;
    
    // Shadow automatically applied via DWM API
    // Creates beautiful floating window effect
}
```

***

### Methods

#### Render()

Manually trigger a full window render.

```csharp
public virtual void Render()
```

**When to use:**

* After changing multiple properties
* After manual theme changes
* To force visual update

**Example:**

```csharp
this.Background = new KtBrushGradient(KtColor.PRIMARY, KtColor.ACCENT);
this.Foreground = KtColor.CONTENT;
this.Render(); // Apply all changes
```

**What it does:**

* Updates ForeColor from Foreground
* Updates BackColor from Background
* Triggers RenderMode() for dark mode
* Invalidates and updates display

***

#### RenderMode()

Updates the window's dark/light mode.

```csharp
public void RenderMode()
```

**Example:**

```csharp
// After theme change
KTheme.Current.Render();
this.RenderMode(); // Update title bar
```

**What it does:**

* Applies native Windows immersive dark mode
* Updates title bar appearance
* Adds shadow for borderless windows
* Sets composited style for flicker-free rendering

***

#### Title()

Get or set the window title.

```csharp
public virtual string Title(string title = null)
```

**Examples:**

```csharp
// Set title
this.Title("My Application");

// Get title
string currentTitle = this.Title();

// Dynamic title updates
this.Title($"Loading... {progress}%");
this.Title($"Processing {currentFile}");
```

***

#### GetForeground()

Gets the effective foreground color.

```csharp
public virtual KtColor GetForeground()
```

**Example:**

```csharp
// Returns Foreground property if set, otherwise ForeColor
KtColor textColor = this.GetForeground();
```

**Use case:**

* When you need the actual foreground color
* For child controls that inherit color
* For custom painting

***

#### Snapshot()

Captures the window as an image.

```csharp
public Image Snapshot()
```

**Example:**

```csharp
// Capture window
Image screenshot = this.Snapshot();

// Save to file
screenshot.Save("window.png");

// Use in picture box
pictureBox1.Image = this.Snapshot();
```

***

#### Mirror()

Captures the screen area behind the window.

```csharp
public virtual (KtWindow _, Bitmap Bitmap) Mirror()
```

**Example:**

```csharp
// Capture what's behind the window
var (window, backgroundImage) = this.Mirror();

// Use for transparency effects
this.BackgroundImage = backgroundImage;
```

**Use case:**

* Creating blur effects
* Transparency effects
* Acrylic/glass effects

***

#### Reset Methods

```csharp
// Reset background to theme default
this.ResetBackColor();

// Reset foreground to theme default
this.ResetForeColor();

// Reset font to KimTools default
this.ResetFont();
```

***

### Advanced Features

#### Theme Change Events

KtWindow automatically subscribes to theme changes.

```csharp
public KtWindow()
{
    InitializeComponent();
    
    // Automatically subscribed to KtColor.ThemeChanged
    // Window updates automatically when theme changes
}
```

**Manual subscription (if needed):**

```csharp
private void OnThemeChanged(bool? isDark)
{
    // Custom logic on theme change
    if (isDark == true)
    {
        // Dark mode specific updates
    }
    else
    {
        // Light mode specific updates
    }
}

// Subscribe
KtColor.ThemeChanged += OnThemeChanged;

// Unsubscribe (done automatically in Dispose)
KtColor.ThemeChanged -= OnThemeChanged;
```

***

#### Property Change Notifications

KtWindow implements `INotifyPropertyChanged`.

```csharp
public partial class KtWindow : Form, INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;
}
```

**Example:**

```csharp
this.PropertyChanged += (sender, e) =>
{
    if (e.PropertyName == nameof(Background))
    {
        // Background changed
    }
};
```

***

#### Custom Paint Background

Override for custom background rendering.

```csharp
protected override void OnPaintBackground(PaintEventArgs e)
{
    base.OnPaintBackground(e);
    
    // Custom painting here if needed
    // KtWindow already handles gradient rendering
}
```

***

#### Native API Optimizations

KtWindow uses several Windows APIs for optimal performance:

**1. DWM (Desktop Window Manager) APIs:**

```csharp
// Dark mode for title bar
DwmSetWindowAttribute(handle, DWMWA_USE_IMMERSIVE_DARK_MODE, ...);

// Shadow for borderless windows
DwmExtendFrameIntoClientArea(handle, margins);
```

**2. Window Styles:**

```csharp
// Composited rendering (hardware accelerated)
WS_EX_COMPOSITED

// Prevents flicker during resize and paint
```

**3. Message Handling:**

```csharp
// Keeps title bar highlighted when active
WM_NCACTIVATE

// Optimized non-client area painting
WM_NCPAINT
```

***

### Best Practices

#### ✅ DO: Use Theme Colors

```csharp
// Good - uses theme colors
this.Background = KtColor.BASE;
this.Foreground = KtColor.CONTENT;

// Adapts automatically to theme changes
```

#### ✅ DO: Use Gradients for Visual Impact

```csharp
// Modern, professional look
this.Background = new KtBrushGradient(
    KtColor.PRIMARY,
    KtColor.ACCENT
);
```

#### ✅ DO: Let Automatic Updates Handle Theme Changes

```csharp
// Don't manually subscribe to theme changes
// KtWindow handles it automatically

public MyWindow()
{
    InitializeComponent();
    // That's it! Automatic theme updates enabled
}
```

#### ❌ DON'T: Call Render() Excessively

```csharp
// Bad - unnecessary renders
this.Background = KtColor.PRIMARY;
this.Render();
this.Foreground = KtColor.CONTENT;
this.Render();

// Good - single render
this.Background = KtColor.PRIMARY;
this.Foreground = KtColor.CONTENT;
this.Render();

// Even better - automatic render
this.Background = KtColor.PRIMARY;  // Calls Render() automatically
this.Foreground = KtColor.CONTENT; // Calls Render() automatically
```

#### ❌ DON'T: Set Opacity in Designer

```csharp
// Opacity is hidden for advanced scenarios
// Use Background transparency instead

// Bad
this.Opacity = 0.5;

// Good - transparent background
var gradient = new KtBrushGradient(
    new KtColor("$Primary", null, 50),  // 50% opacity
    new KtColor("$Accent", null, 50)
);
this.Background = gradient;
```

#### ✅ DO: Use Title() Method

```csharp
// Preferred
this.Title("My Application");

// Also works
this.Text = "My Application";
```

***

### Complete Examples

#### Example 1: Basic Modern Window

```csharp
using KimTools.WinForms;

namespace MyApp.Forms
{
    public partial class MainWindow : KtWindow
    {
        public MainWindow()
        {
            InitializeComponent();
            
            // Set gradient background
            this.Background = new KtBrushGradient(
                KtColor.PRIMARY,
                KtColor.ACCENT
            );
            
            // Set foreground
            this.Foreground = KtColor.CONTENT;
            
            // Set title
            this.Title("My Modern Application");
        }
    }
}
```

***

#### Example 2: Borderless Window with Shadow

```csharp
public partial class SplashScreen : KtWindow
{
    public SplashScreen()
    {
        InitializeComponent();
        
        // Borderless window
        this.FormBorderStyle = FormBorderStyle.None;
        
        // Gradient background
        this.Background = new KtBrushGradient(
            KtColor.PRIMARY,
            KtColor.ACCENT
        );
        
        // Shadow automatically applied!
    }
}
```

***

#### Example 3: Dynamic Theme-Aware Window

```csharp
public partial class SettingsWindow : KtWindow
{
    public SettingsWindow()
    {
        InitializeComponent();
        
        // Use theme colors
        this.Background = KtColor.BASE;
        this.Foreground = KtColor.CONTENT;
        
        // Load theme-specific icons
        UpdateIcons();
    }
    
    private void UpdateIcons()
    {
        if (this.IsDark)
        {
            iconSettings.Image = Resources.SettingsIconDark;
        }
        else
        {
            iconSettings.Image = Resources.SettingsIconLight;
        }
    }
}
```

***

#### Example 4: Window with Progress Title

```csharp
public partial class ProcessingWindow : KtWindow
{
    private Timer progressTimer;
    private int progress = 0;
    
    public ProcessingWindow()
    {
        InitializeComponent();
        
        this.Background = new KtBrushGradient(
            KtColor.PRIMARY,
            KtColor.ACCENT
        );
        
        // Setup progress timer
        progressTimer = new Timer();
        progressTimer.Interval = 100;
        progressTimer.Tick += UpdateProgress;
        progressTimer.Start();
    }
    
    private void UpdateProgress(object sender, EventArgs e)
    {
        progress++;
        
        // Update title with progress
        this.Title($"Processing... {progress}%");
        
        if (progress >= 100)
        {
            progressTimer.Stop();
            this.Title("Processing Complete!");
        }
    }
}
```

***

### Summary

KtWindow provides a complete modern window solution with:

* ✅ **Automatic Dark Mode** - Native Windows 10/11 title bar theming
* ✅ **Gradient Backgrounds** - Beautiful, smooth gradients with any angle
* ✅ **Zero Flicker** - Native API optimizations for smooth rendering
* ✅ **Auto Theme Sync** - Updates automatically when theme changes
* ✅ **Drop Shadows** - Beautiful shadows for borderless windows
* ✅ **Smart Management** - Title updates, snapshots, and more
* ✅ **Easy to Use** - Just inherit from KtWindow and go!

For more information about [KtColor](../utilities/kt-color.md), [KtBrush](../utilities/kt-brush.md), and other KimTools components, refer to their respective documentation.
