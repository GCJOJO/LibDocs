# Dialogue Actions

Every action of a dialogue has two properties :

- **Blocking** : the dialogue waits for this action to finish before playing the next ones.
- **Skippable** : the action can be skipped when the player skips the dialogue with ++esc++.

!!! tip
    You can write and test your dialogues with the [Dialogue Editor](tutorials/3-dialogue-editor.md).

!!! info "Positions and colors"

    - Positions (`x`, `y`) are expressed as a **percentage of the screen**, from `0` (left/top) to `100` (right/bottom).
    - Colors can be a hex string `#RRGGBB` or `#RRGGBBAA` (e.g. `#FF0000` or `#FF000080` for a half-transparent red), or a plain color name : `white`, `black`, `transparent`, `red`, `green` or `blue`.

## Message Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ✅ |

The message action is used to display a message on screen.<br>
The player can click, or press ++enter++ or ++space++, to display the whole message instantly, then again to go to the next action.

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:message",
  "speaker(1)" : "my_datapack:speaker1",
  "text(2)" : "Hello, I am [wave]speaker 1[/wave] !"
}
```

1. The speaker that is speaking, must be one of the speakers defined in the `speakers` array.<br>
2. The text to display. Can be a raw string or a localization key like `dialogue.my_dialogue.line1` (it is translated on the client, in the player's language).<br> The text supports [BBCode tags](../LibLib/Features/9-custom-bbcode-tags.md) and automatically wraps to the next line inside the dialogue box.<br>

</div>

## Choice Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ❌ |

The choice action is used to display a choice on screen.  <br>
The player can choose one of the options, which will result in the next dialogue to be displayed. <br>
The options can also define Save Dialogue and Action fields.<br>

The Save Dialogue field defines which dialogue will be saved to the player's state when the choice is chosen.<br>

The Action field is a string that will be sent to the server when the choice is chosen.  <br>
It can be used to trigger custom events or commands.<br>

!!! warning
    To go to another dialogue, an option must define **both** `next` and `save`. <br>
    If one of them is missing, choosing the option simply closes the dialogue.

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:choice",
  "choices" : [
    {
      "name(1)" : "Option 1",
      "next(2)" : "my_datapack:option_1",
      "save(3)" : "my_datapack:option_1"
    },
    {
      "name" : "Option 2",
      "next" : "my_datapack:option_2",
      "save" : "my_datapack:option_2",
      "action(4)": "do_something"
    },
    {
      "name(5)" : "Leave"
    }
  ]
}
```

1. The name of the option, can be a raw string or a localization key like `option.option1.name`<br>
2. The next dialogue to be displayed when this option is chosen<br>
3. The dialogue to be saved to the player's state when this option is chosen<br>
4. Optional. The action to be sent to the server when this option is chosen<br>
5. An option without `next` and `save` closes the dialogue<br>

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
  "x(1)" : 50.0,
  "y(1)" : 50.0,
  "rotation(2)" : 0.0,
  "scale" : 1.0,
  "color(3)" : "#FFFFFFFF",
  "alignment(4)" : "center"
}
```

1. The position of the text on screen, in percent of the screen : `0` is the left/top of the screen and `100` is the right/bottom. <br> Default is `50` (center of the screen).<br>
2. The rotation of the text in degrees.<br>
3. The color of the text, see [Positions and colors](#dialogue-actions). The alpha of the color is combined with the fade in/out.<br>
4. The alignment of the text, can be `left`, `center` or `right`. Default is `center`.<br>

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
  "x(3)" : 50.0,
  "y(3)" : 50.0,
  "rotation(4)" : 0.0,
  "scale(5)" : 1.0,
  "alpha(6)" : 255
}
```

1. The ID of the image, it is used to reference the image in other actions<br>
2. The image to be displayed, it is a resource location like `my_resourcepack:textures/gui/my_image.png`<br>
3. The position of the center of the image on screen, in percent of the screen : `0` is the left/top of the screen and `100` is the right/bottom.<br>
4. The rotation of the image in degrees, around its center.<br>
5. The scale of the image. At a scale of `1.0` the image takes half of the screen's height, keeping its aspect ratio.<br>
6. The opacity of the image, from `0` (invisible) to `255` (opaque). The image is hidden at `8` or less.<br>

</div>

## Move Image Action

| Blocking | Skippable |
| :---: | :---: |
| ❌ | ✅ |

The move image action animates an image displayed with the [Image Action](#image-action).<br>
Each animation (`position`, `rotation`, `scale` and `color`) is optional and has its own duration (`time`, in ticks) and easing.<br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:image_move",
  "id(1)" : 0,
  "position" : {
    "time" : 20.0,
    "x_start(2)" : 0.0,
    "y_start(2)" : 0.0,
    "x_end(2)" : 100.0,
    "y_end(2)" : 100.0,
    "easing(3)" : "linear"
  },
  "rotation" : {
    "time" : 20.0,
    "from(4)" : 0.0,
    "to(4)" : 360.0,
    "easing(3)" : "linear"
  },
  "scale" : {
    "time" : 20.0,
    "from(5)" : 1.0,
    "to(5)" : 2.0,
    "easing(3)" : "linear"
  },
  "color" : {
    "time" : 20.0,
    "from(6)" : "#FFFFFFFF",
    "to(6)" : "#FFFFFF00",
    "easing(3)" : "linear"
  }
}
```

1. The ID of the image to be moved<br>
2. The position of the image on screen, in percent of the screen : `0` is the left/top of the screen and `100` is the right/bottom.<br>
3. The easing function to be used for the animation, like `linear`, `constant` or `cubic_in_out`. If the easing is unknown, `linear` is used. <br> More info on [Easings](../LibLib/easings.md) <br>
4. The rotation of the image in degrees<br>
5. The scale of the image<br>
6. The color of the image, see [Positions and colors](#dialogue-actions). For now only the alpha of the color is applied to the image : this example fades the image out.<br>

</div>

## Next Dialogue Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ❌ |

The Next Dialogue Action is used to go to the next dialogue.  <br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:next_dialogue",
  "dialogue(1)" : "my_datapack:my_next_dialogue"
}
```

1. The dialogue to go to. The old field name `set` also works.

</div>

## Wait Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ✅ |

The Wait Action is used to wait for a certain amount of time before continuing to the dialogue.<br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:wait",
  "time(1)" : 20.0
}
```

1. Time to wait in ticks.

</div>

## Press Enter Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ❌ |

This action waits for the player to press ++enter++ before continuing the dialogue.<br>
It displays nothing on screen, so it is useful after a [Text Action](#text-action) or an [Image Action](#image-action), to let the player read at their own pace.<br>

```json
{
  "action" : "blablalib:press_enter"
}
```

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

1. The speed at which the letters are displayed on screen, in ticks per letter. <br> Default is 1 tick per letter.<br>
2. The multiplier for the wait time when the character is a punctuation mark (`.`, `!` or `?`). The pause lasts `speed × wait` ticks. <br> Default is 8.<br>

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
  "action" : "blablalib:command",
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
  "to(1)" : "#000000FF",
  "time(2)" : 20.0
}
```

1. The color to fade from and to, see [Positions and colors](#dialogue-actions). If the color is invalid, `transparent` is used.<br>
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
  "cleared_actions(1)" : "blablalib:fade"
}
```

1. Optionally specify the type of action to clear, if not specified all Non-Blocking actions will be cleared.<br>

</div>

## Hide / Show UI Actions

| Blocking | Skippable |
| :---: | :---: |
| ❌ | ✅ |

These actions hide or show the dark gradient drawn behind the dialogue.<br>

```json
{ "action" : "blablalib:hide_ui" }
```

```json
{ "action" : "blablalib:show_ui" }
```

!!! note
    The short versions `hide_ui` and `show_ui` (without the `blablalib:` namespace) also work.

## NPC Action

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ❌ |

This action changes the value of a variable of an [NPC](2-npc.md) for the player in the dialogue.<br>
Changing a variable can make the NPC switch to another state, see [Transition Conditions](2-npc.md#transition-conditions).<br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:npc",
  "npc(1)" : 0,
  "variable(2)" : "has_said_hello",
  "type(3)" : "bool",
  "value(4)" : true
}
```

1. The NPC to modify. `0` is the NPC the player last talked to.<br>
2. The name of the variable, as defined in the NPC Definition.<br>
3. The type of the variable, must be the same as in the NPC Definition. See [Variable Types](2-npc.md#variable-types).<br>
4. The new value of the variable.<br>

</div>

!!! note
    The variable is only changed if the NPC has a variable with this name **and** this type.

## Quest State Action (requires QuestsLib)

| Blocking | Skippable |
| :---: | :---: |
| ✅ | ❌ |

This action changes the state of a quest or of a task for the player in the dialogue.<br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:quest_state",
  "quest" : "my_mod:my_quest",
  "task(1)" : "my_mod:my_task",
  "state(2)" : "started"
}
```

1. Optional. If not specified, the state of the quest is changed.<br>
2. The new state, can be `none`, `started` or `completed`.<br>

</div>

## Play Cutscene Action (requires CutsceneLib)

| Blocking | Skippable |
| :---: | :---: |
| Only if `wait_for_end` is `true` | ❌ |

This action plays a cutscene for the player in the dialogue.<br>

<div class="annotate" markdown>

```json
{
  "action" : "blablalib:play_cutscene",
  "cutscene" : "my_mod:my_cutscene",
  "wait_for_end(1)" : true
}
```

1. Optional, default is `false`. If `true`, the dialogue waits for the end of the cutscene before continuing.<br>

</div>
