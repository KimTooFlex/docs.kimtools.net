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

# 🔹 Kt-TextBox

### Overview

**KtTextBox** is a highly customizable, theme-aware text input control from the KimTools.WinForms SDK that extends the standard Windows Forms TextBox with modern styling, automatic theme adaptation, and advanced features. This control provides multiple visual styles, icon support, loading states, and comprehensive text manipulation capabilities for building contemporary Windows Forms applications.

#### Key Features

* **Multiple Style Presets**: Choose between Tailwind, Fluent, and Material design styles
* **Automatic Theme Integration**: Responds to system theme changes in real-time
* **Icon Support**: Add left and right icons with click handlers
* **Loading State**: Built-in loader indicator for async operations
* **Advanced Text Casing**: Multiple casing options including camelCase, PascalCase, snake\_case, and more
* **Validation Feedback**: Visual error indication for form validation
* **State Management**: Comprehensive state system (Idle, Hover, Active, Disabled)
* **Customizable Borders**: Configurable radius, thickness, and colors

#### Use Cases

* Modern form inputs with theme-aware styling
* Search boxes with icon buttons and loading indicators
* Password fields with show/hide functionality
* Text fields with inline actions (clear, submit, etc.)
* Validated form inputs with visual error feedback
* Multi-line text areas with consistent styling

***

### Properties

#### Appearance Properties

| Property            | Type             | Default      | Description                                              |
| ------------------- | ---------------- | ------------ | -------------------------------------------------------- |
| **Style**           | `KtTextBoxStyle` | `Tailwind`   | Visual style preset (Tailwind, Fluent, Material, Custom) |
| **Bg**              | `KtColor`        | `BASE`       | Background color using KtColor theme system              |
| **Border**          | `KtColor`        | `!BASE % 25` | Border color when idle                                   |
| **BorderActive**    | `KtColor`        | `PRIMARY`    | Border color when focused or active                      |
| **BorderRadius**    | `int`            | `-1` (auto)  | Corner radius in pixels (-1 for style default)           |
| **BorderThickness** | `int`            | `-1` (auto)  | Border width in pixels (-1 for style default, max 5)     |
| **Content**         | `KtColor`        | `!BASE`      | Text color using KtColor theme system                    |

#### Icon Properties

| Property            | Type     | Default    | Description                                |
| ------------------- | -------- | ---------- | ------------------------------------------ |
| **IconLeft**        | `string` | `""`       | Left icon name from KimTools icon library  |
| **IconRight**       | `string` | `""`       | Right icon name from KimTools icon library |
| **CustomIconLeft**  | `Image`  | `null`     | Custom image for left icon                 |
| **CustomIconRight** | `Image`  | `null`     | Custom image for right icon                |
| **IconSize**        | `int`    | `0` (auto) | Icon dimensions in pixels                  |
| **IconStroke**      | `double` | `2.4`      | Icon stroke weight                         |
| **IconPadding**     | `int`    | `10`       | Padding around icons                       |

#### Text Properties

| Property            | Type                  | Default   | Description                                                                                                                |
| ------------------- | --------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Text**            | `string`              | `""`      | The text content of the control. Bindable and localizable                                                                  |
| **TextPlaceholder** | `string`              | `""`      | Placeholder text shown when empty                                                                                          |
| **TextCasing**      | `KtTextCasing`        | `Default` | Automatic text transformation (UpperCase, LowerCase, TitleCase, CamelCase, PascalCase, SnakeCase, KebabCase, SentenceCase) |
| **TextAlign**       | `HorizontalAlignment` | `Left`    | Text alignment (Left, Center, Right)                                                                                       |
| **TextOffsetX**     | `int`                 | `6`       | Horizontal text margin                                                                                                     |
| **TextOffsetY**     | `int`                 | `1`       | Vertical text margin                                                                                                       |
| **TextWrap**        | `bool`                | `true`    | Enable word wrapping in multiline mode                                                                                     |
| **MaxLength**       | `int`                 | `32767`   | Maximum character limit                                                                                                    |

#### Behavior Properties

| Property            | Type   | Default | Description                                        |
| ------------------- | ------ | ------- | -------------------------------------------------- |
| **Enabled**         | `bool` | `true`  | Enable/disable user interaction                    |
| **ReadOnly**        | `bool` | `false` | Prevent text modification while allowing selection |
| **Password**        | `bool` | `false` | Mask input as password characters                  |
| **PasswordChar**    | `char` | `●`     | Character used for password masking                |
| **Loading**         | `bool` | `false` | Show loading indicator and disable input           |
| **ValidationError** | `bool` | `false` | Display error state styling                        |
| **AutoSizeHeight**  | `bool` | `true`  | Automatically adjust height based on font          |

#### Advanced Properties

| Property                     | Type                           | Default | Description                             |
| ---------------------------- | ------------------------------ | ------- | --------------------------------------- |
| **AcceptsReturn**            | `bool`                         | `false` | Allow Enter key in multiline mode       |
| **AcceptsTab**               | `bool`                         | `false` | Allow Tab key input                     |
| **AutoCompleteMode**         | `AutoCompleteMode`             | `None`  | Auto-completion behavior                |
| **AutoCompleteSource**       | `AutoCompleteSource`           | `None`  | Auto-completion data source             |
| **AutoCompleteCustomSource** | `AutoCompleteStringCollection` | `null`  | Custom auto-completion items            |
| **HideSelection**            | `bool`                         | `true`  | Hide selection when control loses focus |
| **ShortcutsEnabled**         | `bool`                         | `true`  | Enable standard keyboard shortcuts      |
| **ScrollBars**               | `ScrollBars`                   | `None`  | Scrollbar visibility in multiline mode  |

#### Read-Only Properties

| Property            | Type         | Description                                   |
| ------------------- | ------------ | --------------------------------------------- |
| **BaseTextBox**     | `TextBox`    | Reference to the underlying TextBox control   |
| **Focused**         | `bool`       | Whether the control currently has input focus |
| **Modified**        | `bool`       | Whether text has been modified since creation |
| **TextLength**      | `int`        | Current text character count                  |
| **SelectedText**    | `string`     | Currently selected text                       |
| **SelectionStart**  | `int`        | Start position of selection                   |
| **SelectionLength** | `int`        | Length of selection                           |
| **Lines**           | `string[]`   | Text split into lines                         |
| **LeftIcon**        | `PictureBox` | Reference to left icon control                |
| **RightIcon**       | `PictureBox` | Reference to right icon control               |

***



### Styles

***

#### KtTextBoxStyle

Visual style presets for the TextBox:

| Value        | Description                                             |
| ------------ | ------------------------------------------------------- |
| **Tailwind** | Default KimTools design with clean borders              |
| **Fluent**   | Microsoft Fluent-inspired design with subtle animations |
| **Material** | Google Material design with underline border            |
| **Custom**   | Fully customizable appearance                           |

#### ktTextBoxState

Control interaction states:

| Value        | Description               |
| ------------ | ------------------------- |
| **Idle**     | Default resting state     |
| **Hover**    | Mouse is over the control |
| **Active**   | Control has focus         |
| **Disabled** | Control is disabled       |

#### KtTextCasing

Automatic text transformation options:

| Value            | Description                            | Example        |
| ---------------- | -------------------------------------- | -------------- |
| **Default**      | No transformation                      | "Hello World"  |
| **UpperCase**    | All uppercase                          | "HELLO WORLD"  |
| **LowerCase**    | All lowercase                          | "hello world"  |
| **TitleCase**    | Capitalize each word                   | "Hello World"  |
| **SentenceCase** | Capitalize first letter                | "Hello world"  |
| **CamelCase**    | First word lowercase, rest capitalized | "helloWorld"   |
| **PascalCase**   | All words capitalized, no spaces       | "HelloWorld"   |
| **SnakeCase**    | Lowercase with underscores             | "hello\_world" |
| **KebabCase**    | Lowercase with hyphens                 | "hello-world"  |

***

### Essential Features

#### 1. Theme-Aware Rendering

KtTextBox automatically subscribes to system theme changes and updates its appearance:

```csharp
KtColor.ThemeChanged += Render;
```

The control intelligently adjusts colors, borders, and icons based on the current theme without requiring manual intervention.

#### 2. Multiple Visual Styles

Choose from preset styles that automatically configure borders, radius, and visual behavior:

* **Tailwind**: Modern, clean design with 2px borders and 10px radius
* **Fluent**: Subtle 1px borders with smooth bottom-line emphasis on focus
* **Material**: Flat design with bottom border only (2px, no radius)

#### 3. State Management System

The control maintains distinct visual states with smooth transitions:

* **Idle**: Default appearance with standard border color
* **Hover**: Subtle color change when mouse enters
* **Active**: Prominent border color when focused
* **Disabled**: Muted appearance with reduced opacity

#### 4. Icon System

Supports both built-in icons and custom images with click handlers:

* Icons automatically recolor based on theme and state
* Icons can function as buttons with event handlers
* Smooth cursor changes for interactive icons
* Automatic layout adjustment for icon presence

#### 5. Loading State

Built-in loader indicator for async operations:

* Animated spinner replaces right icon
* Input becomes read-only during loading
* Wait cursor automatically applied
* Prevents user interaction until complete

#### 6. Validation Integration

Visual feedback for form validation:

* Red border color in error state
* Maintains responsiveness with hover/active states
* Programmatically controllable via `ValidationError` property
* Integrates with `IKtValidate` interface

***

### Examples

#### Basic Text Input

```csharp
var nameInput = new KtTextBox
{
    TextPlaceholder = "Enter your name",
    IconLeft = "user",
    Width = 300,
    Height = 40
};
this.Controls.Add(nameInput);
```

#### Password Field with Toggle

```csharp
var passwordInput = new KtTextBox
{
    TextPlaceholder = "Password",
    Password = true,
    IconLeft = "lock",
    IconRight = "eye",
    Style = KtTextBoxStyle.Tailwind
};

// Toggle password visibility
passwordInput.IconRightClick += (s, e) =>
{
    passwordInput.Password = !passwordInput.Password;
    passwordInput.IconRight = passwordInput.Password ? "eye" : "eye-off";
};
```

#### Search Box with Loading

```csharp
var searchBox = new KtTextBox
{
    TextPlaceholder = "Search...",
    IconLeft = "search",
    IconRight = "x",
    BorderRadius = 20
};

// Clear button
searchBox.IconRightClick += (s, e) =>
{
    searchBox.Clear();
    searchBox.Focus();
};

// Simulate async search
searchBox.TextChanged += async (s, e) =>
{
    if (searchBox.Text.Length < 3) return;
    
    searchBox.Loading = true;
    await PerformSearchAsync(searchBox.Text);
    searchBox.Loading = false;
};
```

#### Email Input with Validation

```csharp
var emailInput = new KtTextBox
{
    TextPlaceholder = "email@example.com",
    IconLeft = "mail",
    TextCasing = KtTextCasing.LowerCase,
    Style = KtTextBoxStyle.Fluent
};

emailInput.TextChanged += (s, e) =>
{
    // Simple email validation
    var isValid = emailInput.Text.Contains("@") && 
                  emailInput.Text.Contains(".");
    emailInput.ValidationError = !isValid && emailInput.Text.Length > 0;
};
```

#### Material Style Multiline

```csharp
var notesInput = new KtTextBox
{
    TextPlaceholder = "Enter your notes...",
    TextArea = true,
    Style = KtTextBoxStyle.Material,
    Height = 120,
    TextWrap = true,
    ScrollBars = ScrollBars.Vertical
};
```

#### Custom Styled Input

```csharp
var customInput = new KtTextBox
{
    Style = KtTextBoxStyle.Custom,
    Bg = KtColor.Base,
    Border = KtColor.Primary % 30,
    BorderActive = KtColor.Primary,
    Content = KtColor.Primary,
    BorderRadius = 8,
    BorderThickness = 2,
    IconLeft = "tag",
    TextPlaceholder = "Custom styled input"
};
```

#### Phone Number with Formatting

```csharp
var phoneInput = new KtTextBox
{
    TextPlaceholder = "(555) 123-4567",
    IconLeft = "phone",
    MaxLength = 14
};

phoneInput.KeyPress += (s, e) =>
{
    // Only allow digits
    if (!char.IsDigit(e.KeyChar) && !char.IsControl(e.KeyChar))
    {
        e.Handled = true;
    }
};
```

#### Username with Case Conversion

```csharp
var usernameInput = new KtTextBox
{
    TextPlaceholder = "username",
    IconLeft = "at-sign",
    TextCasing = KtTextCasing.LowerCase,
    MaxLength = 20
};

usernameInput.KeyPress += (s, e) =>
{
    // Only allow alphanumeric and underscore
    if (!char.IsLetterOrDigit(e.KeyChar) && 
        e.KeyChar != '_' && 
        !char.IsControl(e.KeyChar))
    {
        e.Handled = true;
    }
};
```

#### Auto-Complete Input

```csharp
var countryInput = new KtTextBox
{
    TextPlaceholder = "Select country",
    IconLeft = "globe",
    AutoCompleteMode = AutoCompleteMode.SuggestAppend,
    AutoCompleteSource = AutoCompleteSource.CustomSource
};

var countries = new AutoCompleteStringCollection();
countries.AddRange(new[] { "Kenya", "Uganda", "Tanzania", "Rwanda" });
countryInput.AutoCompleteCustomSource = countries;
```

#### State Change Handling

```csharp
var stateInput = new KtTextBox
{
    TextPlaceholder = "Monitored input"
};

stateInput.StateChanging += (sender, oldState, newState, e) =>
{
    Console.WriteLine($"Changing from {oldState} to {newState}");
    // e.Cancel = true; // Optionally cancel the change
};

stateInput.StateChanged += (sender, newState) =>
{
    Console.WriteLine($"Now in {newState} state");
};
```

#### Dynamic Style Switching

```csharp
var styleInput = new KtTextBox
{
    TextPlaceholder = "Style switcher",
    Style = KtTextBoxStyle.Tailwind
};

var styleButton = new Button { Text = "Switch Style" };
styleButton.Click += (s, e) =>
{
    styleInput.Style = styleInput.Style switch
    {
        KtTextBoxStyle.Tailwind => KtTextBoxStyle.Fluent,
        KtTextBoxStyle.Fluent => KtTextBoxStyle.Material,
        KtTextBoxStyle.Material => KtTextBoxStyle.Tailwind,
        _ => KtTextBoxStyle.Tailwind
    };
};
```

***

### Methods

#### Text Manipulation

| Method                          | Description                              |
| ------------------------------- | ---------------------------------------- |
| `Clear()`                       | Removes all text from the control        |
| `AppendText(string text)`       | Adds text to the end of the current text |
| `SelectAll()`                   | Selects all text in the control          |
| `Select(int start, int length)` | Selects a range of text                  |
| `DeselectAll()`                 | Removes text selection                   |

#### Clipboard Operations

| Method    | Description                   |
| --------- | ----------------------------- |
| `Copy()`  | Copies selection to clipboard |
| `Cut()`   | Moves selection to clipboard  |
| `Paste()` | Inserts clipboard content     |

#### Undo/Redo

| Method        | Description                       |
| ------------- | --------------------------------- |
| `Undo()`      | Undoes the last operation         |
| `ClearUndo()` | Clears the undo buffer            |
| `CanUndo()`   | Returns whether undo is available |

#### Position and Navigation

| Method                                | Description                           |
| ------------------------------------- | ------------------------------------- |
| `GetCharFromPosition(Point pt)`       | Gets character at specified location  |
| `GetCharIndexFromPosition(Point pt)`  | Gets character index at location      |
| `GetPositionFromCharIndex(int index)` | Gets location of character index      |
| `GetLineFromCharIndex(int index)`     | Gets line number from character index |
| `GetFirstCharIndexFromLine(int line)` | Gets first character index of line    |
| `GetFirstCharIndexOfCurrentLine()`    | Gets first character of current line  |
| `ScrollToCaret()`                     | Scrolls to show the caret position    |

#### State and Validation

| Method                           | Description                          |
| -------------------------------- | ------------------------------------ |
| `HasText()`                      | Returns whether text is not empty    |
| `IsEmpty()`                      | Returns whether text is empty        |
| `State()`                        | Gets the current visual state        |
| `State(params ktTextBoxState[])` | Checks if state matches any provided |
| `Focus()`                        | Sets input focus to the control      |

#### Layout and Rendering

| Method                                | Description                              |
| ------------------------------------- | ---------------------------------------- |
| `Render()`                            | Redraws the control with current state   |
| `Render(ktTextBoxState state)`        | Renders with specific state              |
| `Render(KtRenderCondition condition)` | Renders under specific condition         |
| `ResizeControl()`                     | Adjusts control to appropriate size      |
| `Reset()`                             | Resets to default state with placeholder |
| `ResetText()`                         | Resets Text property to default          |

***

### Events

| Event                    | Description                                     |
| ------------------------ | ----------------------------------------------- |
| **TextChanged**          | Occurs when the Text property value changes     |
| **TextChange**           | Alternate event for text changes                |
| **StateChanged**         | Occurs after the control's visual state changes |
| **StateChanging**        | Occurs before state change (cancelable)         |
| **IconLeftClick**        | Occurs when the left icon is clicked            |
| **IconRightClick**       | Occurs when the right icon is clicked           |
| **KeyDown**              | Occurs when a key is first pressed              |
| **KeyPress**             | Occurs when a key is pressed and released       |
| **KeyUp**                | Occurs when a key is released                   |
| **EnabledChanged**       | Occurs when the Enabled property changes        |
| **AcceptsTabChanged**    | Occurs when AcceptsTab property changes         |
| **BorderStyleChanged**   | Occurs when BorderStyle property changes        |
| **HideSelectionChanged** | Occurs when HideSelection property changes      |
| **ModifiedChanged**      | Occurs when Modified property changes           |
| **ReadOnlyChanged**      | Occurs when ReadOnly property changes           |
| **TextAlignChanged**     | Occurs when TextAlign property changes          |



### Implementation Notes

#### Designer Integration

* Appears in Visual Studio Toolbox as **"@KimTools ▪ TextBox"**
* Properties organized under **" 🗲 KimTools"** category&#x20;
* Full design-time experience with live preview
* Default property: `Text`, Default event: `TextChanged`

#### Performance Optimization

* Suspended rendering during layout operations
* Double-buffered to prevent flicker
* Efficient state change detection
* Optimized icon rendering with caching
* Lazy evaluation of visual properties

#### Border and Radius Behavior

When set to `-1` (automatic), borders and radius adapt to the selected style:

* **Tailwind**: 2px border, 10px radius
* **Fluent**: 1px border, 10px radius
* **Material**: 2px border, 0px radius (flat)

#### Text Casing Implementation

Text casing uses extension methods for transformation:

* Handles Unicode characters appropriately
* Preserves original input in backing field
* Updates display text dynamically
* Efficient string manipulation

***

### Best Practices

1. **Use appropriate styles**: Choose styles that match your application's design language
2. **Leverage theme colors**: Use `KtColor` values for automatic dark/light mode support
3. **Handle loading states**: Always set `Loading = true` during async operations
4. **Validate input**: Use `ValidationError` for visual feedback on invalid entries
5. **Icon as buttons**: Attach event handlers to icons for clear/submit actions
6. **Text casing**: Use automatic casing for consistent data formatting
7. **Placeholder text**: Provide clear, concise placeholder guidance
8. **State management**: Monitor state changes for advanced UI behaviors
9. **Dispose properly**: Ensure proper disposal when removing controls programmatically
10. **Test both themes**: Verify appearance in both light and dark modes

***

### Related Resources

* [**KtColor Utility**](https://www.kimtoo.net/sdk/utilities/kt-color): Theme-aware color system used by this control
* [**KtBrush Utility**](https://www.kimtoo.net/sdk/utilities/kt-brush): Advanced brush and painting utilities
* [**KimTools Icon Library**](https://www.kimtoo.net/sdk/kt-icons): Complete icon reference for IconLeft/IconRight properties
