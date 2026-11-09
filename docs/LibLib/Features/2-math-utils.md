# Math Utils

## Lerp Functions

The math utils provide a set of lerp functions that can be used to interpolate between two values.<br>
The lerp functions are available for different data types, such as

- `float`
- `double`
- `integer`
- `Vec2`
- `Vec3`
- `Vector3f`
- `Color`

## Clamp Functions

The math utils provide a set of clamp functions that can be used to clamp a value between a minimum and maximum value.<br>
The clamp functions are available for different data types, such as

- `float`
- `double`
- `integer`

## Degrees to Radians and Radians to Degrees Functions

Functions to convert between degrees and radians are also provided.<br>
Works with `float`, and `double`.

## Color

The `Color` class represents an RGBA color, with each channel between `0` and `255`.

```java
Color red = new Color(255, 0, 0, 255);        // red, green, blue, alpha
Color fromInt = new Color(0xFFFF0000);        // ARGB integer
int argb = red.getColorInt();                 // back to an ARGB integer
```

Predefined colors : `Color.WHITE`, `Color.BLACK`, `Color.TRANSPARENT`, `Color.RED`, `Color.GREEN` and `Color.BLUE`.

### Parsing colors from strings

`Color.fromString(String)` parses a color from a string, and returns `null` if the string is invalid.<br>
`Color.fromString(String, Color)` does the same but returns the given fallback color instead of `null`.

Supported formats :

| Format | Example | Result |
| --- | --- | --- |
| `#RRGGBB` | `#FF0000` | Opaque red |
| `#RRGGBBAA` | `#FF000080` | Half-transparent red |
| Color name | `red` | `white`, `black`, `transparent`, `red`, `green` or `blue` |

!!! warning
    8 digits hex colors are read as `#RRGGBBAA` (the alpha is **last**), unlike Minecraft's ARGB integers.
