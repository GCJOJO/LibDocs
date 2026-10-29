# Player Data Storage

The Library provides a way to store data for a player in a Mod-Loader Agnostic way.
To store data for a player, you need to create a class that extends the `PlayerSaveData` class and register it inside the `PlayerDataRegistry` class.

## Creating a PlayerSaveData class

Here is a simple example of a `PlayerSaveData` class that stores the number of cookies a player has eaten.

<div class="annotate" markdown>
```java
public class MyPlayerSaveData extends PlayerSaveData {
    public int playerCookies = 0;

    @Override
    public CompoundTag serialize() {
        CompoundTag nbt = new CompoundTag();
        nbt.putInt("playerCookies", playerCookies);
        return nbt;
    }

    @Override
    public void deserialize(CompoundTag nbt) {
        playerCookies = nbt.getInt("playerCookies");
    }
}
```

Now we can register it during our mod initialization :

```java
// Mod Initialization
PlayerDataRegistry.register(MyPlayerSaveData.class, MyPlayerSaveData::new);
```

To get the data for a player and modify it, you can do as follows :
```java
MyPlayerSaveData data = LibLib.getPlayerDataManager().deserializePlayerData(player, "my_player_save_data", MyPlayerSaveData.class); //(1)
data.playerCookies++;
LibLib.getPlayerDataManager().serializePlayerData(player, data, "my_player_save_data"); //(2)
```

1. Loads the data for the player, if it doesn't exist, it will create a new instance of `MyPlayerSaveData` and return it.
2. Saves the data for the player.

</div>
