<!-- md:version 8.0.0 -->
<!-- md:feature -->

# Datapack Creation

First create a data pack using this folder structure
<div class="annotate" markdown>
```
.
├─ datapack/
│  ├─ my_datapack/
│  │  ├─ dialogues/
│  │  │  ├─ my_dialogues.json
│  │  │  ├─ my_other_dialogues.json
│  │  │  ├─ the_best_dialogues_youve_ever_seen.json
│  │  │  └─ ... (1)
```
</div>
1.  You can many different dialogue files.

# Creating Speakers

Inside any dialogue file you can define the different speakers that may speak in your dialogues.

<div class="annotate" markdown>
```json
{
  "speakers" : [
    { "id(1)" : "my_datapack:speaker1", "name(2)": "Speaker 1", "color(3)": "FFFFFFFF", "sounds(4)" : [] },
    { "id(1)" : "my_datapack:speaker2", "name(2)": "Speaker 2", "color(3)": "FFFF0000", "sounds(4)" : ["block.note_block.banjo"] },
    { "id(1)" : "my_datapack:speaker3", "name(2)": "Speaker 3", "color(3)": "FFFFFFFF", "sounds(4)" : ["block.note_block.xylophone", "block.note_block.flute", "block.note_block.basedrum", "block.mud.fall"] },
  ]
}
```
</div>

1.   The unique identifier of the speaker
2.   The name of the speaker, can be a raw string or a localization key like `speaker.speaker1.name`
3.   The color of the speaker's name
4.   The sounds the dialogue will make when a letter appears on screen. If there are multiple sounds, a random one will be chosen for each letter. 

# Creating Dialogues

<div class="annotate" markdown>
```json
{
  "my_dialogue" : [
    { 
      "action(1)" : "blablalib:message", 
      "speaker(2)" : "my_datapack:speaker1", 
      "text(3)" : "Hello, I am speaker 1 !"
    },
    { 
      "action" : "blablalib:message", 
      "speaker" : "my_datapack:speaker2", 
      "text" : "Hello, I am speaker 2 !"
    }
  ],

  "my_other_dialogue" : [
    { 
      "action" : "blablalib:message", 
      "speaker" : "my_datapack:speaker3", 
      "text" : "Hello, I am speaker 3 !"
    }
  ]
}
```

1. The action to perform, in this case display a message on screen.
2. The speaker that is speaking, must be one of the speakers defined in the speakers array
3. The text to display on screen, can be a raw string or a localization key like `dialogue.my_dialogue.line1`

</div>

To read more about the different actions you can perform in a dialogue, check out the [Actions](../actions.md) page.