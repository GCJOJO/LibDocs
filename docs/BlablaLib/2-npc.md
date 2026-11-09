# NPCs

BlablaLib implements a custom NPC System and Entity. <br>
To create your NPC Entity just use the `/summon` command : 

``/summon blablalib:npc ~ ~ ~ {Definition:"my_mod_id:my_custom_npc_definition"}``

But wait, what is a NPC Definition ?

## NPC Definitions

NPC Definition are a way to describe your NPCs.
They should look like this : 

<div class="annotate" markdown>

```json
{
  "name(1)": "Bob",
  "variables(2)": [
    {
      "type(3)": "bool",
      "name(4)": "has_said_hello",
      "default_value": false
    }
  ],
  "root_state(5)" : "idle",
  "states": [
    {
      "state_name": "idle",
      "dialogue(6)" : "blablalib:test_npc_first_dialogue",
      "visual_state(7)": {
        "model(8)": "blablalib:geometry.npc",
        "texture": "blablalib:textures/entity/npc/default.png",
        "animation": "idle"
      },
      "transitions(9)": [
        {
          "target_state(10)": "has_said_hello",
          "condition": {
            "type(11)": "blablalib:equals",
            "variable" : "has_said_hello",
            "value" : true
          }
        }
      ]
    },
    {
      "state_name": "has_said_hello",
      "dialogue" : "blablalib:test_npc_said_hello",
      "visual_state": {
        "model": "blablalib:geometry.npc",
        "texture": "blablalib:textures/entity/npc/default.png",
        "animation": "talk"
      },
      "transitions": [

      ]
    }
  ]
}
```

1. The name that will be displayed above your NPC's head
2. Here you can define the different variables of your NPC
3. [Here](#variable-types) is a complete list of variable type
4. This is the name of the variable, you will use this name to reference the variable and getting or setting it's value
5. The default state of your NPC
6. The dialogue that will be played if the NPC is in that state
7. The Visual State describre the physical appearance of your NPC
8. The Model of your NPC must be a model defined inside of your ressource pack : `assets/<my_mod_id>/npc_models/my_model.geo.json` You use the model ID defined inside of the file to refenrce your model
9. Here you can define the different transition this state will be able to do.
10. The target state of the transition
11. The type of the condition. [Here](#transition-conditions) for more info.

</div>

!!! warning "Renamed field"
    The default value of a variable is now defined with `default_value` (it used to be `defaultValue`). <br>
    Update your old NPC Definitions, otherwise the variables will fail to load.

## Per-Player State

Each player has their own state for every NPC : the current state and the values of the variables are stored **per player**.<br>
For example, if a player talks to Bob and `has_said_hello` becomes `true`, Bob will still be in his `idle` state for the other players.

The state of each player is saved with the NPC entity (in its `PlayerData` NBT tag), so it is kept when the world is reloaded.<br>
When the NPC is loaded, its visual state is sent again to every connected player.

## Changing Variables from a Dialogue

The variables of an NPC can be modified from a dialogue using the [NPC Action](1-actions.md#npc-action) :

```json
{
  "action" : "blablalib:npc",
  "npc" : 0,
  "variable" : "has_said_hello",
  "type" : "bool",
  "value" : true
}
```

## Variable Types

Currently there are 4 variable types :

### Boolean

Type Name : `bool`<br>
Values : `true` or `false`

### Number

Type Name : `number`<br>
Values : any numerical values (integer or decimal)

### String

Type name : `string`<br>
Values : any text

### Resource Location

Type name : `resource_location`<br>
Values : a valid Resource Location 

## Transition Conditions

To transition from different states, you must use conditions

Here is a list of the different conditions : 

### Equal Condition

This condition verifies if the variable and the value you defined are the same.
```json
"condition": 
{
    "type": "blablalib:equals",
    "variable" : "my_variable",
    "value" : "Bob"
}
```

### Numerical Conditions

There are 4 Numerical Conditions : Less, Less than or Equal, Greater, Greater than of Equal
<div class="annotate" markdown>
```json
"condition": 
{
    "type(1)": "blablalib:greater",
    "variable" : "my_numerical_variable",
    "value" : 50
}
```

1. Can be `"blablalib:less_than_or_equal"`, `"blablalib:less"`, `"blablalib:greater"`, `"blablalib:greater_than_or_equal"`

</div>

### Is In Dialogue Condition

This condition verifies if the player is currently in a dialogue
```json
"condition": 
{
    "type": "blablalib:is_in_dialogue"
}
```

### Not Condition

The condition verifies if the inner condition is false.

```json
"condition": 
{
    "type": "blablalib:not",
    "inner" : {
        "type" : "blablalib:is_in_dialogue"
    }
}
```

### And / Or Condition

Verifies if the different inner conditions are all true for the And Condition or just one is true for the Or Condition.

<div class="annotate" markdown>
```json
"condition": 
{
    "type(1)": "blablalib:and",
    "conditions" : [
        {
            "type" : "blablalib:is_in_dialogue"
        },
        {
            "type" : "blablalib:equals",
            "variable" : "my_variable",
            "value" : "Bob"
        }
    ]
}
```

1. Can be `blablalib:and` or `blablalib:or`

</div>

### XOR Condition 

This condition verifies that only one of the two inner conditions is true.

```json
"condition": 
{
    "type": "blablalib:xor",
    "conditions" : [
        {
            "type" : "blablalib:is_in_dialogue"
        },
        {
            "type" : "blablalib:equals",
            "variable" : "my_variable",
            "value" : "Bob"
        }
    ]
}
```

### Count Condition

This condition verifies that a minimum amount of inner conditions are true

```json
"condition": 
{
    "type": "blablalib:count",
    "required_amount" : 2,
    "conditions" : [
        {
            "type" : "blablalib:is_in_dialogue"
        },
        {
            "type" : "blablalib:equals",
            "variable" : "my_variable",
            "value" : "Bob"
        },
        {
            "type" : "blablalib:greater",
            "variable" : "my_other_variable",
            "value" : 5
        }
    ]
}
```

### Random Condition

This condition generates a random number in the range 0 to 1 and checks wether it is greater than the chance value.

```json
"condition" : 
{
    "type" : "blablalib:random",
    "chance" : 0.3
}
```

### Quest Condition (requires QuestsLib)

Checks wheter a Quest or Task is in the specific State

<div class="annotate" markdown>

```json
"condition" : 
{
    "type" : "blablalib:quest",
    "quest" : "my_mod:my_quest",
    "task(1)" : "my_mod:my_task",
    "state(2)" : "completed"
}
```

1. Optional. If not specified, the target of the condition will be the quest.
2. Optional. By default is `completed`. Can be `none`, `started` or `completed`.

</div>