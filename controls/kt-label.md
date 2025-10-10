# 🔹 Kt-Label

## KtLabel Control Documentation

### Overview

**KtLabel** is an enhanced label control from the KimTools.WinForms SDK that extends the standard Windows Forms `Label` with theme-aware color management. This control automatically adapts to light/dark theme changes and provides a simplified, theme-integrated approach to text display in modern Windows Forms applications.

#### Key Features

* **Automatic Theme Integration**: Responds to system theme changes in real-time
* **Simplified Color Management**: Uses KtColor for consistent theming across your application
* **Transparent Background**: Automatically sets transparent background for seamless UI integration
* **Parent Color Inheritance**: Inherits parent control colors when no explicit color is set

#### Use Cases

* Display static or dynamic text with automatic theme adaptation
* Create labels that match your application's color scheme automatically
* Build accessible UI elements that respond to system dark/light mode changes
* Simplify color management in complex forms with hierarchical color inheritance

***

### Properties

| Property  | Type      | Default         | Description                                                                                                                              |
| --------- | --------- | --------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Text**  | `string`  | `""`            | The text content displayed by the label. Localizable and bindable to settings.                                                           |
| **Color** | `KtColor` | `KtColor.Empty` | The theme-aware color for the label text. Uses KtColor enumeration for automatic theme adaptation. Values are constrained to 0-99 range. |

#### Property Details

**Color Property**



* Accepts `KtColor` enumeration values (constrained via modulo 100 operation)
* When set to `KtColor.Empty`, inherits color from parent control
* Automatically updates when system theme changes
* See [KtColor Documentation](https://www.kimtoo.net/sdk/utilities/kt-color) for available color values

***

### Events

> _Note: Standard Label events remain available (Click, TextChanged, etc.)_

***

### Essential Features

#### 1. Theme-Aware Rendering

KtLabel automatically subscribes to theme change events and updates its appearance accordingly:

When the system switches between light and dark modes, all KtLabel instances update their colors automatically without requiring code intervention.

#### 2. Intelligent Color Inheritance

The control implements a smart color resolution system:

1. If `Color` is set to a specific `KtColor` value, use that color
2. If `Color` is `KtColor.Empty`, inherit from parent control's `ForeColor`
3. Fallback to current `ForeColor` if no parent is available

#### 3. Transparent Integration

The label automatically sets its background to transparent, ensuring seamless integration with parent containers:

***

### Examples

#### Basic Usage

```csharp
// Create a label with automatic theme color
var label = new KtLabel
{
    Text = "Welcome to KimTools",
    Color = KtColor.Primary, // Uses primary theme color
    AutoSize = true
};
this.Controls.Add(label);
```

#### Theme-Adaptive Label

```csharp
// Label that adapts to parent's color scheme
var headerLabel = new KtLabel
{
    Text = "Application Header",
    Color = KtColor.Empty, // Inherits from parent
    Font = new Font("Segoe UI", 16, FontStyle.Bold),
    Dock = DockStyle.Top
};
```

#### Status Indicator Label

```csharp
// Create status labels with semantic colors
var successLabel = new KtLabel
{
    Text = "✓ Operation Successful",
    Color = KtColor.Success
};

var errorLabel = new KtLabel
{
    Text = "✗ Operation Failed",
    Color = KtColor.Error
};

var warningLabel = new KtLabel
{
    Text = "⚠ Warning: Check Configuration",
    Color = KtColor.Warning
};
```

#### Dynamic Color Updates

```csharp
// Update label color based on application state
private void UpdateStatusLabel(bool isConnected)
{
    statusLabel.Text = isConnected ? "Connected" : "Disconnected";
    statusLabel.Color = isConnected ? KtColor.Success : KtColor.Error;
    // Color automatically renders based on current theme
}
```

#### Localized Content

```csharp
// The Text property supports localization
var localizedLabel = new KtLabel
{
    Text = Resources.WelcomeMessage, // From resource file
    Color = KtColor.Primary
};
```

#### Container with Multiple Labels

```csharp
// Create a panel with color-coordinated labels
var infoPanel = new Panel();

var titleLabel = new KtLabel
{
    Text = "System Information",
    Color = KtColor.Primary,
    Font = new Font("Segoe UI", 12, FontStyle.Bold),
    Location = new Point(10, 10)
};

var detailLabel = new KtLabel
{
    Text = "Version 2.0.1",
    Color = KtColor.Empty, // Inherits from panel
    Location = new Point(10, 40)
};

infoPanel.Controls.AddRange(new Control[] { titleLabel, detailLabel });
```

***

***

### Best Practices

1. **Use KtColor.Empty for inheritance**: Allow labels to inherit colors from their container for consistent theming
2. **Leverage theme events**: The control handles theme changes automatically—no manual intervention needed
3. **Semantic colors**: Use appropriate KtColor values (Success, Error, Warning) for status indicators
4. **Dispose properly**: When removing labels programmatically, ensure proper disposal to prevent memory leaks
5. **Test both themes**: Verify your UI works correctly in both light and dark modes
