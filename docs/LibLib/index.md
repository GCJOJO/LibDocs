# Getting Started with LibLib

## Features

LibLib is a library for Minecraft 1.21.1 for NeoForge and Fabric.<br>
This library adds features such as : <br>

- APIs for dependent mods: BlablaLibAPI, CutsceneLibAPI, and QuestsLibAPI.
- UI Utilities :
    - Hierarchical UI System
    - Stylized text system (bbcode)
- Camera System
    - `/camera` command
    - Camera Movement
    - Fade In/Out
    - Screen Shakes
- Tweening System
- Backported Mannequins from 1.21.9
- Persistent Player Data Storage System
- Custom Events
- Math Utilities

## As a Player

This mod does not add anything by itself, it is a library other mods depends on.<br>
If no mod depends on this library in your modpack, you don't need to install LibLib.

Download the more on [Curseforge](https://www.curseforge.com/minecraft/mc-mods/liblib) or [Modrinth](https://modrinth.com/mod/liblib-gcjojo).

## As a Mod Developer

Simply add this to your build.gradle file to add LibLib as a dependency for your mod.

```groovy title="build.gradle"
repositories{
    maven {
        url 'https://jitpack.io'
        content { includeGroup "com.github.GCJOJO.LibLib" }
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
    modImplementation "com.github.GCJOJO.LibLib:LibLib-common:${liblib_version}"
    
    // Fabric
    // You do need to depend on Architectury to use the custom events.
    modImplementation "dev.architectury:architectury-fabric:${architectury_api_version}"
    modImplementation "com.github.GCJOJO.LibLib:liblib-fabric:${liblib_version}"

    // NeoForge
    // You do need to depend on Architectury to use the custom events.
    modImplementation "dev.architectury:architectury-forge:${architectury_api_version}"
    modImplementation "com.github.GCJOJO.LibLib:LibLib-neoforge:${liblib_version}"

    // For NeoForge you need to add these as runtimeLibraries otherwise the mod will crash
    forgeRuntimeLibrary "org.incendo:cloud-annotations:${cloud_annotations_version}"

    forgeRuntimeLibrary ("org.incendo:cloud-core:${cloud_core_version}") { transitive = false }
    forgeRuntimeLibrary ("org.incendo:cloud-services:${cloud_core_version}") { transitive = false }
    forgeRuntimeLibrary ("org.incendo:cloud-brigadier:${cloud_version}") { transitive = false }

    forgeRuntimeLibrary "io.leangen.geantyref:geantyref:1.3.16"
}
```