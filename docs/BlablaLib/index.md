# Welcome to BlablaLib

BlablaLib is a library for Minecraft 1.21.1 for NeoForge and Fabric
It adds supports for data-driven dialogues.

# Installing the Mod as a Player

This mods does not add anything by itself, it is a library other mods depends on.<br>
If no mod depends on this library in your modpack, you don't need to install BlablaLib.

Download the mod on [Curseforge](https://www.curseforge.com/minecraft/mc-mods/blablalib) or on [Modrinth](https://modrinth.com/mod/blablalib).


If you are a Modpack Developer you can install this mod and write a datapack to create your own dialogues.
Follow the tutorial [here](tutorials/creating_dialogues.md) for more info.

# Installing as a Dependency for your mod

You must depend on Architectury to use the custom events.

```groovy title="build.gradle"
plugins {
    //...
    id 'architectury-plugin' version '3.4-SNAPSHOT'
}

architectury {
    minecraft = project.minecraft_version
}

repositories{
    maven {
        url 'https://jitpack.io'
        content { includeGroup "com.github.GCJOJO.BlablaLib" }
    }

    //For fabric only
    maven {
        name = "Ladysnake Mods"
        url = 'https://maven.ladysnake.org/releases'
    }
}

dependencies {
    // Common (if using Architectury)
    modImplementation "dev.architectury:architectury:$rootProject.architectury_api_version"
    modImplementation "com.github.GCJOJO.BlablaLib:BlablaLib-common:${blablalib_version}"
    
    // Fabric
    modImplementation "dev.architectury:architectury-fabric:${architectury_api_version}"
    modImplementation "com.github.GCJOJO.BlablaLib:blablalib-fabric:${blablalib_version}"

    // NeoForge
    modImplementation "dev.architectury:architectury-forge:${architectury_api_version}"
    modImplementation "com.github.GCJOJO.BlablaLib:blablalib-forge:${blablalib_version}"
}
```

