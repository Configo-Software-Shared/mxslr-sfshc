# Salesforce Formula Syntax Highlighting

This module provides comprehensive syntax highlighting and prettification for Salesforce formulas. It includes functions for displaying formulas with proper formatting, syntax highlighting, and copy functionality.

## Features

- **Robust Tokenizer**: Parses formulas into distinct tokens for reliable highlighting
- **Comprehensive Function Support**: 150+ Salesforce functions across all categories
- **Comment Support**: Handles both `/* */` block comments and `//` line comments
- **Operator Recognition**: Properly recognizes multi-character operators (`&&`, `||`, `<=`, `>=`, `<>`)
- **Nested Field References**: Supports `[Account].[Name]` and `[Account.Name]` syntax
- **Custom Function Support**: Recognizes custom Apex functions (lowercase identifiers)
- **Formula Field References**: Highlights references to other formula fields
- **Error Highlighting**: Detects and highlights syntax errors and invalid functions
- **Dark Mode Support**: Alternative color scheme for dark backgrounds
- **Custom Themes**: User-selectable color schemes (Light, Dark, Solarized, Monokai)
- **Line Numbers**: Optional line numbering for complex formulas
- **Collapsible Sections**: Ability to collapse/expand long formula sections
- **Prettification**: Consistent formatting and capitalization
- **Copy Functionality**: One-click copy buttons for formulas
- **DataTable Integration**: Ready-to-use render functions for tables
- **Responsive Design**: Works well in various container sizes

## Quick Start

### 1. Include the Script

Make sure the script is included in your HTML:

```html
<script type="text/javascript" src="script/cfg-sfdc-tokens.js"></script>
```

### 2. Initialize Support

The script auto-initializes when the page loads, but you can also call it manually in specific scenarios:

```javascript
initializeSalesforceFormulaSupport();
```

**Manual initialization is useful for:**

- **Dynamic content loading**: When formulas are added after page load
- **Single Page Applications**: When content changes without page refresh
- **Conditional loading**: When formulas should only be initialized under certain conditions
- **Error recovery**: If auto-initialization failed or was interrupted
- **Testing/Debugging**: For testing different initialization scenarios

### 3. Use the Functions

#### Basic Code Block Creation

```javascript
const formula = 'IF([Status] = "Active", "Yes", "No")';
const html = createFormulaCodeBlock(formula, {
  prettify: true,
  showCopyButton: true,
});
document.getElementById("container").innerHTML = html;
```

#### DataTable Integration

```javascript
const table = initDataTable("#myTable", true, {
  columns: [
    { data: "name", title: "Name" },
    {
      data: "formula",
      title: "Formula",
      render: renderSalesforceFormula(true, false),
    },
  ],
});
```

## API Reference

### `tokenizeFormula(formula)`

Tokenizes a Salesforce formula into an array of tokens.

**Parameters:**

- `formula` (string): The Salesforce formula to tokenize

**Returns:** (Array) Array of token objects with type, value, and position

### `classifyTokens(tokens)`

Classifies tokens into specific types (function, constant, etc.).

**Parameters:**

- `tokens` (Array): Array of tokens from tokenizeFormula

**Returns:** (Array) Array of classified tokens

### `renderTokens(tokens)`

Renders tokens as HTML with syntax highlighting.

**Parameters:**

- `tokens` (Array): Array of classified tokens

**Returns:** (string) HTML string with syntax highlighting

### `highlightFormula(formula)`

Main function to highlight a Salesforce formula.

**Parameters:**

- `formula` (string): The Salesforce formula to highlight

**Returns:** (string) HTML string with syntax highlighting

### `prettifySalesforceFormula(formula)`

Prettifies a Salesforce formula by applying consistent formatting.

**Parameters:**

- `formula` (string): The raw Salesforce formula

**Returns:** (string) The prettified formula

**Example:**

```javascript
const raw = 'if(and(status="active",priority="high"),"urgent","normal")';
const pretty = prettifySalesforceFormula(raw);
// Result: "IF (AND ([Status] = "Active", [Priority] = "High"), "Urgent", "Normal")"
```

### `createFormulaCodeBlock(formula, options)`

Creates a complete syntax-highlighted code block for a Salesforce formula.

**Parameters:**

- `formula` (string): The Salesforce formula
- `options` (object, optional):
  - `prettify` (boolean): Whether to prettify the formula first (default: true)
  - `className` (string): Additional CSS classes
  - `showCopyButton` (boolean): Whether to show a copy button (default: true)

**Returns:** (string) HTML for the code block

**Example:**

```javascript
const html = createFormulaCodeBlock('IF([Status] = "Active", "Yes", "No")', {
  prettify: true,
  showCopyButton: true,
  className: "my-custom-class",
});
```

### `renderSalesforceFormula(prettify, showCopyButton)`

Creates a DataTable render function for Salesforce formulas.

**Parameters:**

- `prettify` (boolean): Whether to prettify the formula (default: true)
- `showCopyButton` (boolean): Whether to show copy button in table cells (default: false)

**Returns:** (Function) DataTable render function

**Example:**

```javascript
const table = initDataTable("#myTable", true, {
  columns: [
    { data: "name", title: "Name" },
    {
      data: "formula",
      title: "Formula",
      render: renderSalesforceFormula(true, false),
    },
  ],
});
```

## Syntax Highlighting Colors

The following color scheme is used for syntax highlighting:

- **Functions** (blue): `IF`, `AND`, `OR`, `TEXT`, `LEFT`, etc.
- **Constants** (orange): `TRUE`, `FALSE`, `NULL`, `BLANK`, `EMPTY`
- **Operators** (gray): `=`, `<>`, `+`, `-`, `*`, `/`, `&&`, `||`, etc.
- **Field References** (green): `[FieldName]`
- **Nested Field References** (dark green, underlined): `[Account].[Name]`, `[Account.Name]`
- **Custom Functions** (purple, italic): `calculateDiscount()`, `getAccountType()`
- **Formula Field References** (orange, highlighted): `Total_Amount_Calculated`
- **Strings** (pink): `"text"` or `'text'`
- **Numbers** (blue): `123`, `45.67`
- **Comments** (gray italic): `/* comment */` or `// comment`
- **Errors** (red, strikethrough): Invalid functions and syntax errors
- **Dot Notation** (gray): `.` in nested field references

## Phase 3 Features

### Dark Mode Support

The system includes a complete dark mode color scheme:

```javascript
// Switch to dark mode
setFormulaTheme("dark");

// Switch back to light mode
setFormulaTheme("light");
```

### Custom Themes

Four built-in themes are available:

- **Light**: Default light theme with high contrast
- **Dark**: Dark theme for low-light environments
- **Solarized**: Easy on the eyes with reduced contrast
- **Monokai**: High contrast theme with vibrant colors

### Line Numbers

Add line numbers to complex formulas for better readability:

```javascript
const html = createFormulaCodeBlock(formula, {
  prettify: true,
  showLineNumbers: true,
});
```

### Collapsible Sections

Long formulas can be collapsed to save space:

```javascript
const html = createFormulaCodeBlock(formula, {
  prettify: true,
  showCollapseToggle: true,
});
```

### Theme API

```javascript
// Get current theme
const currentTheme = getCurrentTheme();

// Get available themes
const themes = getAvailableThemes();

// Set theme
setFormulaTheme("dark");
```

### Enhanced Options

The `createFormulaCodeBlock` function now supports additional options:

```javascript
const html = createFormulaCodeBlock(formula, {
  prettify: true,
  showCopyButton: true,
  showLineNumbers: true, // Add line numbers
  showThemeSelector: true, // Add theme dropdown
  showCollapseToggle: true, // Add collapse toggle
  maxLines: 5, // Limit height to 5 lines
});
```

## Phase 2 Features

### Nested Field References

The system now supports complex nested field references:

```javascript
// Bracket notation
IF([Account].[Name] = "Test Account", "Valid", "Invalid")

// Dot notation
CASE([Account.Name], "Customer", "C", "Partner", "P", "Unknown")

// Complex nested references
TEXT([Account].[Owner].[Name]) + " - " + [Account].[Type]
```

### Custom Function Support

Custom Apex functions are recognized and highlighted:

```javascript
// Custom function with parameters
calculateDiscount([Amount], [Discount_Percentage])

// Custom function in conditional logic
IF(getAccountType([AccountId]) = "Premium", "High Priority", "Standard")

// Mixed standard and custom functions
IF(calculateDiscount() > 0, "Discount Applied", "No Discount")
```

### Formula Field References

References to other formula fields are highlighted with special styling:

```javascript
// Single formula field reference
Total_Amount_Calculated + Tax_Amount_Calculated;

// Formula field in conditional logic
IF(Total_Amount_Calculated > 1000, "High Value", "Standard Value");

// Multiple formula field references
Discount_Amount + Tax_Amount + Shipping_Amount;
```

### Error Highlighting

The system detects and highlights various types of errors:

```javascript
// Invalid function (not in Salesforce function list)
INVALIDFUNC([Account].[Name])

// Unmatched parentheses
IF([Status] = "Active", "Yes"

// Unmatched brackets
[Account.Name + " - " + [Type]

// Multiple errors
INVALIDFUNC([Account.Name + "Test"
```

## Supported Salesforce Functions

The syntax highlighter recognizes the following categories of Salesforce functions:

### Logical Functions

- `AND`, `OR`, `NOT`, `IF`, `CASE`, `SWITCH`
- `XOR`, `NAND`, `NOR`
- `ISNULL`, `ISBLANK`, `ISNUMBER`, `ISTEXT`, `ISDATE`, `ISCHANGED`, `PRIORVALUE`

### Text Functions

- `TEXT`, `LEFT`, `RIGHT`, `MID`, `LEN`, `FIND`, `SUBSTITUTE`
- `TRIM`, `UPPER`, `LOWER`, `PROPER`, `BR`, `HYPERLINK`, `IMAGE`, `VALUE`
- `CONTAINS`, `BEGINS`, `INCLUDES`, `EXCLUDES`
- `REGEX`, `REGEX_REPLACE`, `SPLIT`, `JOIN`, `REPLACE`
- `REPT`, `CLEAN`, `CODE`, `CHAR`, `UNICHAR`, `UNICODE`

### Math Functions

- `ABS`, `CEILING`, `FLOOR`, `ROUND`, `MOD`, `MAX`, `MIN`
- `SQRT`, `EXP`, `LN`, `LOG`, `POWER`, `RAND`
- `SIN`, `COS`, `TAN`, `ASIN`, `ACOS`, `ATAN`
- `PI`, `DEGREES`, `RADIANS`, `SIGN`, `FACT`, `GCD`, `LCM`

### Date/Time Functions

- `TODAY`, `NOW`, `DATE`, `DATETIMEVALUE`, `DATEVALUE`
- `YEAR`, `MONTH`, `DAY`, `HOUR`, `MINUTE`, `SECOND`, `WEEKDAY`
- `ADDMONTHS`, `MONTHS_BETWEEN`, `DAYS_BETWEEN`, `HOURS_BETWEEN`, `MINUTES_BETWEEN`, `SECONDS_BETWEEN`
- `DATEADD`, `DATEDIFF`, `DATETIME_FORMAT`, `TIMEVALUE`, `TIMENOW`, `TIMETONUM`, `NUMTOTIME`
- `CALENDAR_MONTH`, `CALENDAR_QUARTER`, `CALENDAR_YEAR`, `FISCAL_MONTH`, `FISCAL_QUARTER`, `FISCAL_YEAR`

### Type Conversion and Validation

- `VALUE`, `TEXT`, `BLANKVALUE`, `NULLVALUE`, `CURRENCY`, `NUMBER`, `DOUBLE`, `INT`, `LONG`

### Advanced Functions

- `CHOOSE`, `COALESCE`, `IFNULL`, `NVL`, `DECODE`
- `GREATEST`, `LEAST`, `RANK`, `DENSE_RANK`, `ROW_NUMBER`
- `LAG`, `LEAD`, `FIRST_VALUE`, `LAST_VALUE`

## Comment Support

The system supports both block comments and line comments:

### Block Comments

```javascript
IF(([Status] = "Active") /* Check if account is active */, "Yes", "No");
```

### Line Comments

```javascript
IF(([Priority] = "High"), "Urgent", "Normal"); // Handle priority levels
```

### Multi-line Comments

```javascript
/*
 * Complex validation rule for customer accounts
 * Checks multiple conditions and assigns appropriate status
 */
IF(AND(([Type] = "Customer"), [Amount] >= 1000), "VIP", "Standard");
```

## Operator Recognition

The system properly recognizes all Salesforce operators:

### Comparison Operators

- `=`, `<>`, `<`, `>`, `<=`, `>=`

### Logical Operators

- `&&` (AND), `||` (OR)

### Arithmetic Operators

- `+`, `-`, `*`, `/`, `&` (concatenation)

## Demo Pages

Several demo pages are available to test the functionality:

- **`cfg-sfdc-index.html`**: The index page for all other test pages
- **`cfg-sfdc-tokenizer-test.html`**: Interactive tokenization testing
- **`cfg-sfdc-datatable-demo.html`**: DataTable integration examples
- **`cfg-sfdc-phase2-features-test.html`**: Phase 2 advanced features testing
- **`cfg-sfdc-phase3-features-test.html`**: Phase 3 visual enhancements testing
- **`cfg-sfdc-operator-fix-verification.html`**: Multi-character operator verification
- **`cfg-sfdc-debug-tokenization.html`**: Tokenization debugging and analysis
- **`cfg-sfdc-prettify-test.html`**: Prettification process debugging

## Integration with Validation Rules

When you're ready to add validation rules to your reports, you can use these functions to display the validation rule formulas with proper syntax highlighting:

```javascript
// Example for validation rule display
function displayValidationRule(rule) {
  return `
    <div class="ui segment">
      <h4>${rule.name}</h4>
      <p><strong>Error Message:</strong> ${rule.errorMessage}</p>
      <p><strong>Formula:</strong></p>
      ${createFormulaCodeBlock(rule.formula, {
        prettify: true,
        showCopyButton: true,
      })}
    </div>
  `;
}
```

## Technical Architecture

### Tokenizer-Based Approach

The system uses a robust tokenizer that:

1. **Parses** the formula into distinct tokens
2. **Classifies** each token (function, field, operator, etc.)
3. **Renders** tokens as HTML with appropriate styling

This approach ensures:

- **No overlapping replacements**: Each character is processed exactly once
- **Reliable highlighting**: No broken HTML or escaped entities
- **Easy debugging**: Visual feedback at every step
- **Extensible**: Easy to add new token types or modify rules

### Token Types

- `FUNCTION`: Salesforce functions (IF, AND, TEXT, etc.)
- `FIELD`: Field references in square brackets
- `NESTED_FIELD`: Nested field references ([Account].[Name])
- `CUSTOM_FUNCTION`: Custom Apex functions (lowercase)
- `FORMULA_FIELD`: References to other formula fields
- `OPERATOR`: Operators (=, <>, &&, ||, etc.)
- `STRING`: String literals in quotes
- `NUMBER`: Numeric values
- `CONSTANT`: Constants (TRUE, FALSE, NULL, etc.)
- `COMMENT`: Comments (/\* \*/ and //)
- `ERROR`: Syntax errors and invalid functions
- `DOT`: Dot notation in nested fields
- `PARENTHESIS`: Parentheses
- `COMMA`: Commas
- `WHITESPACE`: Spaces, tabs, newlines
- `IDENTIFIER`: Other identifiers

## Browser Compatibility

- Modern browsers with ES6 support
- Includes fallback for clipboard API in older browsers
- Responsive design works on mobile and desktop

## Customization

You can customize the appearance by modifying the CSS classes in the `addFormulaSyntaxStyles()` function or by overriding the styles in your own CSS.

## Performance

The tokenizer approach is highly efficient:

- **O(n)** time complexity for tokenization
- **Minimal memory usage** with streaming tokenization
- **Cached results** for repeated formulas
- **Optimized rendering** with efficient HTML generation
