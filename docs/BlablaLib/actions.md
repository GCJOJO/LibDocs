# Dialogue Actions

## Message Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ✅ | 

The message action is used to display a message on screen.

```json
{
  "action" : "blablalib:message",
  "speaker" : "my_datapack:speaker1",
  "text" : "Hello, I am speaker 1 !"
}
```

## Choice Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ❌ | 

The choice action is used to display a choice on screen.  <br>
The player can choose one of the options, which will result in the next dialogue to be displayed. <br>
The options can also define Save Dialogue and Action fields.<br>

The Save Dialogue field defines which dialogue will be saved to the player's sate when the choice is choosen.<br>

The Action field is a string that will be sent to the server when the choice is choosen.  <br>
It can be used to trigger custom events or commands.<br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:choice",
  "choices" : [
    {
      "name(1)" : "Option 1",
      "next(2)" : "my_datapack:option_1"
    },
    {
      "name" : "Option 2",
      "next" : "my_datapack:option_2",
      "save(3)" : "my_datapack:option_2",
      "action(4)": "do_something"
    }
  ]
}
```

1. The name of the option, can be a raw string or a localization key like `option.option1.name`<br>
2. The next dialogue to be displayed when this option is choosen<br>
3. The dialogue to be saved to the player's state when this option is choosen<br>
4. The action to be sent to the server when this option is choosen<br>

</div>

## Text Action

| Blocking | Skippable |
| :---: | :---: |
| ❌ | ✅ |

The text action is used to display a text on screen.  <br>
All fields are optional except for the text field.<br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:text",
  "text" : "Hello, I am a text !",
  "fade_in_time" : 1.0,
  "hold_time" : 2.0,
  "fade_out_time" : 1.0,
  "x(1)" : 0.5,
  "y(1)" : 0.5,
  "rotation" : 0.0,
  "scale" : 1.0,
  "color(2)" : "#FFFFFFFF",
  "alignment(3)" : "center"
}
```

1. The position of the text on screen, can be a float between 0.0 and 1.0, where 0.0 is the left/top of the screen and 1.0 is the right/bottom of the screen<br>
2. The color of the text, can be a hex string like `#FFFFFFFF` or a plain color name like `white`, `black`, `transparent`, `red`, `green`, or `blue` <br>
3. The alignment of the text, can be `left`, `center` or `right`<br>

</div>

## Image Action

| Blocking | Skippable |
| :---: | :---: |
| ❌ | ✅ |

The image action is used to display an image on screen.  <br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:image",
  "id(1)" : 0,
  "image(2)" : "my_resourcepack:textures/gui/my_image.png",
  "width" : 100,
  "height" : 100,
  "x(3)" : 0.5,
  "y(3)" : 0.5,
  "rotation" : 0.0,
  "scale" : 1.0,
  "alpha" : 255
}
```

1. The ID of the image, it is used to reference the image in other actions<br>
2. The image to be displayed, it is a resource location like `my_resourcepack:textures/gui/my_image.png`<br>
3. The position of the text on screen, can be a float between 0.0 and 1.0, where 0.0 is the left/top of the screen and 1.0 is the right/bottom of the screen<br>

</div>

## Move Image Action

| Blocking | Skippable |
| :---: | :---: |
| ❌ | ✅ |

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:move_image",
  "id(1)" : 0,
  "position" : {
    "time" : 1.0,
    "x_start(2)" : 0.0,
    "y_start(2)" : 0.0,
    "x_end(2)" : 1.0,
    "y_end(2)" : 1.0,
    "easing(3)" : "linear"
  },
  "rotation" : {
    "time" : 1.0,
    "from(4)" : 0.0,
    "to(4)" : 360.0,
    "easing(3)" : "linear"
  },
  "scale" : {
    "time" : 1.0,
    "from(5)" : 1.0,
    "to(5)" : 2.0,
    "easing(3)" : "linear"
  },
  "color" : {
    "time" : 1.0,
    "from(6)" : "#FFFFFFFF",
    "to(6)" : "#FF000000",
    "easing(3)" : "linear"
  }
}
```

1. The ID of the image to be moved<br>
2. The position of the image on screen, can be a float between 0.0 and 1.0, where 0.0 is the left/top of the screen and 1.0 is the right/bottom of the screen<br>
3. The easing function to be used for the animation, can be `linear`, `constant`, `cubic_in_out`. <br> More info on [Easings](../LibLib/easings.md) <br>
4. The rotation of the image in degrees<br>
5. The scale of the image<br>
6. The color of the image, can be a hex string like `#FFFFFFFF` or a plain color name like `white`, `black`, `transparent`, `red`, `green`, or `blue` <br>

</div>

## Next Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ❌ |

The Next Action is used to go to the next dialogue.  <br>

```json
{
  "action" : "blablalib:next",
  "next" : "my_datapack:my_next_dialogue"
}
```

## Wait Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ✅ |

The Wait Action is used to wait for a certain amount of time before continuing to the dialogue.<br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:wait",
  "time(1)" : 20.0,
}
```

1. Time to wait in ticks.

</div>

## Timings Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ❌ |

This action is used to set the timings for the dialogue.  <br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:timings",
  "speed(1)" : 3,
  "wait(2)" : 10
}
```

1. The speed at which the letters are displayed on screen, in ticks per letter. <br> Default if 1 tick per letter.<br>
2. The multiplier for the wait time when the caracter is a punctuation mark. <br> Default is 8.<br>

</div>

## Sound Action

| Blocking | Skippable |
| :---: | :---: |
| ❌ | ✅ |

This actions plays a sound.<br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:sound",
  "sound(1)" : "minecraft:block.note_block.banjo",
  "pitch(2)" : 1.0,
  "volume(3)" : 1.0
}
```

1. The sound to be played, it is a resource location like `minecraft:block.note_block.banjo`<br>
2. The pitch of the sound, default is 1.0<br>
3. The volume of the sound, default is 1.0<br>

</div>

## Execute Command Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ❌ |


This action executes a command on the server.<br>
Since dialogues are server-side, the client cannot ask the server to execute a command.<br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:execute_command",
  "command(1)" : "say Hello, from <PLAYER>!"
}
```

1. The command to be executed on the server.<br> The command is executed inside a `/execute positioned as <PLAYER> rotated as <PLAYER> run` command, so you can use relative coordinates and the player's rotation.<br> You can also use the `<PLAYER>` placeholder to refer to the player that is currently in the dialogue.<br>

</div>

## Fade Action

| Blocking | Skippable |
| :---: | :---: |
| ❌ | ✅ |

This action fades the screen to a color.<br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:fade",
  "from(1)" : "#00000000",
  "to(1)" : "#FFFFFFFF",
  "time(2)" : 20.0
}
```

1. The color to fade from and to, can be a hex string like `#FFFFFFFF` or a plain color name like `white`, `black`, `transparent`, `red`, `green`, or `blue` <br>
2. The time to fade in ticks.<br>

</div>

## Clear Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ✅ |

This actions clears all Non-Blocking actions from the screen, or specific types of actions if specified.<br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:clear",
  "cleared_action(1)" : "blablalib:fade",
}
```

1. Optionally specify the type of action to clear, if not specified all Non-Blocking actions will be cleared.<br>

</div>