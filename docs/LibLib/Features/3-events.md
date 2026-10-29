# Events
The Library provides multiple events.

- `PLAYER_CHANGED_CHUNK` : Triggered when a player changes chunk. Provides the `ServerPlayer` and the new `ChunkPos`.
- `PLAYER_ENTERED_BIOME` : Triggered when a player enters a new biome. Provides the `ServerPlayer` and the new biome's `ResourceLocation`.
- `PLAYER_ENTERED_STRUCTURE` : Triggered when a player enters a new structure. Provides the `ServerPlayer` and the new structure's `ResourceLocation`.
- `PLAYER_INVENTORY_CHANGED` : Triggered when a player's inventory changes. Provides the `ServerPlayer` and a `Map<ResourceLocation, Integer>` representing the difference in the player's inventory.
- `PRE_FRAME_RENDER` : Triggered before each frame is rendered. Provides a `DeltaTracker` that can be used to get the delta time between frames.