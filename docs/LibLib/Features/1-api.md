# APIs

LibLib provides APIs for dependent mods to use. The following APIs are available:

- [BlablaLibAPI](#blablalibapi) : An API for creating playing dialogues.
- [CutsceneLibAPI](#cutscenelibapi) : An API for playing cutscenes.
- [QuestsLibAPI](#questslibapi) : An API for interacting with the quests system.

These APIs only work if the mod is installed alongside your mod.

# BlablaLibAPI
BlablaLibAPI is an API for playing dialogues.<br>
It allows you to open a dialogue for a player, set the current dialogue, check if a player is in a dialogue, get the last read dialogue for a player, and set the last read dialogue for a player.<br>
It also provides an event that is triggered when a dialogue is completed.

Methods : 

- `openDialogue(ServerPlayer player, ResourceLocation dialogueId)` : Opens a dialogue for the specified player.
- `setCurrentDialogue(ServerPlayer player, ResourceLocation dialogueId)` : Sets the current dialogue for the specified player.
- `isPlayerInDialogue(ServerPlayer player)` : Checks if the specified player is in a dialogue.
- `getPlayerLastReadDialogue(ServerPlayer player)` : Gets the last read dialogue for the specified player.
- `setPlayerLastReadDialogue(ServerPlayer player, ResourceLocation lastReadDialogueId)` : Sets the last read dialogue for the specified player.
     
Events :

- `DialogueCompletedEvent` : An event that is triggered when a dialogue is completed. It provides the player and the dialogue ID that was completed.

# CutsceneLibAPI

CutsceneLibAPI is an API for playing cutscenes.<br>
It allows you to play a cutscene for a player or a collection of players, with an optional anchor position and rotation.

Methods :

- `playCutscene(ServerPlayer player, ResourceLocation cutsceneId)` : Plays a cutscene for the specified player. The anchor position and rotation will be the player's current position and rotation.
- `playCutscene(ServerPlayer player, ResourceLocation cutsceneId, Vec3 anchorPosition, Vector3f anchorRotation)` : Plays a cutscene for the specified player with an anchor position and rotation.
- `playCutscene(Collection<ServerPlayer> players, ResourceLocation cutsceneId)` : Plays a cutscene for the specified collection of players. The anchor position and rotation will be the players' current position and rotation.
- `playCutscene(Collection<ServerPlayer> players, ResourceLocation cutsceneId, Vec3 anchorPosition, Vector3f anchorRotation)` : Plays a cutscene for the specified collection of players with an anchor position and rotation.

# QuestsLibAPI

QuestsLibAPI is an API for interacting with the quests system.<br>
It allows you to start a quest for a player, set the completion state of a quest or task for a player, check if a quest is completed for a player, get the completion percentage of a quest for a player, and get the current task of a quest for a player.<br>

<div class="anotate" markdown>
Methods :

- `startQuest(Player player, ResourceLocation questId)` : Starts a quest for the specified player.
- `setQuestCompletionState(Player player, ResourceLocation questId, String newState)`: Sets the completion state of a quest for the specified player.
- `setTaskCompletionState(Player player, ResourceLocation questId, ResourceLocation taskId, String newState)` : Sets the completion state of a task for the specified player.
- `isQuestCompleted(Player player, ResourceLocation questId)` : Checks if a quest is completed for the specified player.
- `getQuestCompletion(Player player, ResourceLocation questId)` : Gets the completion percentage of a quest for the specified player.
- `getCurrentTask(Player player, ResourceLocation questId)` : Gets the current task of a quest for the specified player.

Events :

- `QUEST_COMPLETED` : An event that is triggered when a quest is completed. It provides a `ServerPlayer` and the quest ID that was completed.
- `TASK_COMPLETED` : An event that is triggered when a task is completed. It provides a `ServerPlayer`, the quest ID, and the task ID that was completed.

!!! note "Quest and Task State Values"

    The state of the quest or task, can be one of the following : `none`, `started`, `completed`.

</div>