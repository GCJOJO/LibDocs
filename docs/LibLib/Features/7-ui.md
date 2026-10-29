# UI

LibLib implements a hierarchical UI system that allows mod developers to create custom user interfaces for their mods.<br>
This system is designed to be flexible and easy to use, enabling developers to create complex UI layouts.<br>

Each UI element can be customized with various properties, such as position, rotation, size and more for each element.<br>
Elements can also be hold child elements, allowing for the creation of complex UI hierarchies.<br>

## Basic Element Functions

```java
setPosition(Vec2 position);
setAngle(float angle);
setSize(Vec2 size);
setScale(Vec2 scale);
setColor(Color color);
setVisible(boolean visible);
setWidth(float width);
setHeight(float height);

getPosition();
getAngle();
getSize();
getScale();
getColor();
getWidth();
getHeight();
getScaledWidth();
getScaledHeight();
draw(GuiGraphics graphics, double mouseX, double mouseY, float partialTick, Vec2 parentPosition);

addChild(GuiElement child);
getChild(int index);
removeChild(GuiElement child);
clearChildren();

focus();
isFocused();
unfocus();
```

## GuiScreen

This class directly inherits from `Screen` and can be used to create custom screens for your mod.<br>
You can add or remove elements from the screen, and it will handle rendering and input for you.<br>