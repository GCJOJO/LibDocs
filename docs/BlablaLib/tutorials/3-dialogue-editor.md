# Using the Dialogue Editor

[**BlablaLib Editor**](https://gcjojo.github.io/BlablaLib-Editor/){ target="_blank" } is a web editor for BlablaLib dialogues.<br>
It lets you write dialogues with forms instead of raw JSON, and plays them in a **preview** that behaves like the mod in game.

[Open the editor :material-open-in-new:](https://gcjojo.github.io/BlablaLib-Editor/){ .md-button .md-button--primary target="_blank" }

!!! info "Your files stay on your computer"
    The editor runs entirely in your browser : nothing is sent to a server. <br>
    Your work in progress is kept in the browser's storage, so you can close the tab and come back later.

## The interface

The editor is made of four parts :

- **The top bar** : project name, undo / redo (++ctrl+z++ / ++ctrl+y++), the language of the preview, the list of issues, and the buttons to open, import, save and export your files. The gear icon opens the **Options**, where you can change the language of the site (English or French).
- **The sidebar** on the left, with four tabs :
    - **Dialogues** : your dialogue files and the dialogues they contain. You can search, create, rename, duplicate and delete dialogues.
    - **Speakers** : the speakers of the project, shared between all the files.
    - **Translations** : the keys of your `lang` files, for each language.
    - **Extensions** : the custom actions of other mods, see [Extensions](#extensions).
- **The action list** in the middle : the actions of the selected dialogue, in order. Click an action to edit it in its form.
- **The preview** on the right, with the **playback log** below it.

## Starting a project

You have three ways to start :

=== "Open a folder (Chrome / Edge)"

    Click **Open a folder** and select a datapack, or the `resources` folder of a mod.<br>
    The editor finds :

    - the dialogues in `data/<namespace>/dialogues/*.json`
    - the translations in `assets/<namespace>/lang/*.json`
    - the textures in `assets/<namespace>/textures/**.png`

    Folders like `build` or `run` are ignored.<br>
    **Save** only rewrites the files you changed, directly in your folder.

=== "Import files (all browsers)"

    Import one or several dialogue JSON files.<br>
    When you are done, click **Export** to download a `.zip` : the datapack is at its root, and the translations and textures are in a `resourcepack/` folder.

=== "Start from scratch"

    Create a **New empty project**, then add a file and your first dialogue from the sidebar.

!!! note
    Opening a folder uses a browser feature only available in Chrome and Edge. On Firefox, import your files and use **Export** instead.

## Writing a dialogue

1. Create your [speakers](1-creating-dialogues.md#creating-speakers) in the **Speakers** tab : name, name color and typing sounds.
2. In the **Dialogues** tab, create a dialogue.
3. Click **Add an action** and pick an action in the palette. The actions are grouped by category (Visual, Pacing, Game).
4. Fill the form of the action. Each field has a short help text, and the color fields have a color picker.
5. Drag and drop the actions to reorder them.

Each action shows whether it is **blocking** and **skippable**, just like in the [Actions](../1-actions.md) page.

### Message text

The text field of the [Message Action](../1-actions.md#message-action) has buttons to insert the [BBCode tags](../../LibLib/Features/9-custom-bbcode-tags.md) (bold, italic, shake, wave, rainbow, gradient...).<br>
It also shows the automatic line wrapping and warns you when the text overflows the dialogue box.

### Translations

A text can be plain text or a translation key. When the text matches a key of your `lang` files, the editor shows its translation.<br>
Use the language selector of the top bar to preview the dialogue in another language.

## Previewing a dialogue

The preview plays the selected dialogue like the mod does : click, ++space++ or ++enter++ to advance a message, ++enter++ for a [Press Enter Action](../1-actions.md#press-enter-action), ++esc++ to skip.

The preview controls let you :

- replay from the start, pause and resume, or advance one tick at a time
- change the playback speed
- **play from a given action** of the list
- follow the selected action
- simulate the network of the mod (actions are sent by batches, with one tick of latency)
- import a screenshot of your world as the background, change the resolution and GUI scale, or go fullscreen

The **playback log** lists what happens : sounds, commands, choices, NPC and quest changes, cutscenes...

!!! warning "Limits of the preview"
    - Sounds and commands are only written in the log, they are not played.
    - The length of cutscenes is simulated.
    - Custom BBCode effects from other mods are ignored.
    - The font and buttons are redrawn : the letter widths are the game's, but not the exact drawing.

## Issues

The editor checks your dialogues while you write them, and lists the issues in the top bar and under each action. For example :

- a speaker or a dialogue that doesn't exist
- an invalid color or texture
- a choice option without `next` **and** `save`
- an action that would crash the game, or leave the player stuck in the dialogue
- actions that will never be played because they come after a choice or a [Next Dialogue Action](../1-actions.md#next-dialogue-action)

Some issues come with a button to fix them automatically, like renaming a wrong field.

!!! tip
    The editor reproduces the behaviour of the code of BlablaLib, **including its bugs**. If an issue says that something will not work in game, trust it.

## Extensions

Mods can add their own actions with [`registerCustomAction`](2-extensions.md). The editor doesn't know them, so it shows them as unknown actions.<br>
An **extension** is a JSON file that describes these actions, without any code : their fields, and whether they are blocking or skippable. The editor then shows them in the palette with a form and checks.

In the **Extensions** tab, you can create an extension, import one provided with a mod, or export yours to share it with the users of your mod.

```json
{
  "format": 1,
  "id": "my_mod",
  "name": "My mod",
  "version": "1.0.0",
  "actions": [
    {
      "id": "my_mod:camera_shake",
      "label": "Camera shake",
      "description": "Shakes the player's camera.",
      "icon": "zap",
      "blocking": true,
      "skippable": true,
      "preview": { "mode": "ticks", "ticksField": "time", "log": "intensity {intensity}" },
      "fields": [
        { "key": "time", "label": "Duration", "type": "number", "required": true, "default": 20, "min": 0, "step": 1, "hint": "In ticks." },
        { "key": "intensity", "label": "Intensity", "type": "number", "default": 1, "min": 0, "max": 5, "step": 0.1, "slider": true }
      ]
    }
  ]
}
```

- The field types are `text`, `multiline`, `number`, `bool`, `select`, `color`, `dialogue`, `speaker`, `texture` and `json`.
- The preview doesn't run the Java code of the action. It only reproduces its pacing with `preview.mode` : `instant` (passes immediately), `ticks` (lasts a number of ticks) or `input` (waits for a click or a key), and writes it in the log.
- With a folder open, extensions are saved in a `blablalib-extensions/` folder. They are not exported in the datapack : the game doesn't need them.
- If an extension is removed, its actions become unknown actions again, without losing their data.

The full format is described in the [editor's repository](https://github.com/GCJOJO/BlablaLib-Editor/blob/dev/docs/plan-extensions.md).
