# UI Elements

## GuiText

This element is used to display text on the screen.<br>

Fields:

- `text` - The text to display, a Component (can be a Literal or a Translatable like `gui.my_mod.my_text`)<br>
- `HorizontalAlignment` - The horizontal alignment of the text, can be `LEFT`, `CENTER` or `RIGHT`<br>
- `VerticalAlignment` - The vertical alignment of the text, can be `TOP`, `CENTER` or `BOTTOM`<br>

## GuiRichText

This element is used to display rich text on the screen.<br>
Supports [BBCode](https://en.wikipedia.org/wiki/BBCode) formatting, allowing for standard BBCode featurs such as colors, bold, italic.<br>
LibLib provides [custom BBCode tags](9-custom-bbcode-tags.md) for additional features, such as shake, wave, tornado, rainbow, gradient and pulse.<br>

Same fields as `GuiText`, but also supports the following additional fields:

- `textWidth` - The width of the text area, if the text exceeds this width it will wrap to the next line.<br>

## GuiImage

This element is used to display an image on the screen.<br>

When constructing a `GuiImage`, you need to provied the image's dimensions.<br>

Fields:

- `imagePath` - The path to the image, a ResourceLocation<br>
- `imageHorizontalAlignment` - The horizontal alignment of the image, can be `LEFT`, `CENTER` or `RIGHT`<br>
- `imageVerticalAlignment` - The vertical alignment of the image, can be `TOP`, `CENTER` or `BOTTOM`<br>

## GuiButton

A button element that can be clicked by the user.<br>

When constructing a `GuiButton`, you need to provide the button's content (a Component) and optionally the click calback.<br>

## GuiColorRect

This element is used to display a colored rectangle on the screen.<br>

When constructing a `GuiColorRect`, you need to provide the color of the rectangle as well as its corners.<br>

