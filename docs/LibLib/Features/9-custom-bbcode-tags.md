# LibLib BBCode Tags

LibLib provides new BBCode Tags inspired by Godot.

These include : 

- `[shake intensity=<value> speed=<value>]` : By default, `intensity=2.0` and `speed=1.0`
- `[wave amplitude=<value> frequency=<value> speed=<value>]` : By default, `amplitude=3.0`, `frequency=0.3` and `speed=5.0`
- `[tornado radius=<value> speed=<value>]` : By default, `radius=3.0` and `speed=4.0`
- `[rainbow speed=<value> saturation=<value> brightness=<value>]` : By default, `speed=0.3`, `saturation=0.8` and `brightness=1.0`
- `[gradient from=<color> to=<color>]` : By default, `from=#FFFFFFFF` (white) and `to=#000000FF` (black)

Colors use the same format as [`Color.fromString`](2-math-utils.md#color) : `#RRGGBB`, `#RRGGBBAA` or a color name like `red`.

Example :

```
[gradient from=#FF0000 to=#0000FF]Hello World ![/gradient]
```