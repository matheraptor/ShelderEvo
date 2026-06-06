# HIMS Console CSS Documentation

## Overview

The `consoleCSS` method is a utility within the `HIMS` prototype used to generate CSS style strings for the browser's DevTools console. These strings are passed to `console.log` using the `%c` directive to create a formatted "System Dashboard" aesthetic.

## Method Signature

```javascript
HIMS.prototype.consoleCSS = function(options)
```

### Parameters

The method accepts a single `options` object with the following properties:

| Property     | Type        | Default       | Description                                                      |
|:-------------|:------------|:--------------|:-----------------------------------------------------------------|
| `color`      | `hex_color` | `"white"`     | The color of the text (e.g., `"#7EFF00"`).                       |
| `weight`     | `String`    | `"bold"`      | The thickness of the font (e.g., `"bold"`, `"900"`, `"normal"`). |
| `background` | `String`    | `"black"`     | The background color of the log entry.                           |
| `family`     | `String`    | `"monospace"` | The font family (e.g., `"Consolas"`, `"Courier New"`).           |
| `padding`    | `String`    | `"0px"`       | Internal spacing around the text.                                |

### Return Value

Returns a **String** containing a valid CSS rule set.

---

## Possible Values & Recommendations

### 1. Color (`color`)

- **Standard GO**: `"#7EFF00"` (Bright Green)
- **Critical FAIL**: `"#ff073a"` (Bright Red)
- **Info/Neutral**: `"gray"` or `"#C0C0C0"`
- **Cyber Blue**: `"#00BFFF"`

### 2. Font Weight (`weight`)

- **Heavy**: `"900"` or `"bold"`
- **Standard**: `"400"` or `"normal"`
- **Light**: `"100"`

### 3. Background (`background`)

- **Deep Space**: `"black"` or `"#000000"`
- **Dark Gray**: `"#1a1a1a"`
- **Alert Red**: `"#ff073a"` (Use with white text for high-visibility errors)

### 4. Font Family (`family`)

- **Terminal Look**: `"monospace"`, `"Consolas"`, `"Courier New"`, `"Lucida Console"`
- **Clean Look**: `"Arial"`, `"Helvetica"`, `"sans-serif"`

### 5. Padding (`padding`)

- **None**: `"0px"`
- **Tight**: `"2px 5px"`
- **Spacious**: `"5px 10px"`

---

## Implementation Example

### Basic Usage

```javascript
const style = $HIMS.consoleCSS({ color: "#7EFF00" });
console.log("%cSYSTEM READY", style);
```

### Advanced "Alert" Badge

```javascript
const alertStyle = $HIMS.consoleCSS({
    color: "white",
    weight: "900",
    background: "#ff073a",
    padding: "2px 10px",
    family: "monospace"
});
console.log("%cCRITICAL FAILURE", alertStyle);
```
