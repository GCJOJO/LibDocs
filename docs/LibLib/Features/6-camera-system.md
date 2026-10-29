# Camera System

LibLib adds a camera system to Minecraft, allowing for cinematic camera movements and effects.<br>
This system can be used by mod developers to create cutscenes, dynamic camera angles, and immersive experiences within their mods.<br>
It comes with the addition of the `/camera` command, which allows players to control the camera directly in-game.
There are also commands and APIs to hide the HUD and/or the player's hand, and block the player's input (keyboard and/or mouse).

## Camera Command Syntax

<div class="annotate" markdown>
```bash
camera <target> set pos <pos> rot <yaw> <pitch> <roll> #(1)!
camera <target> set pos <pos> #(2)!
camera <target> set rot <yaw> <pitch> <roll> #(3)!
camera <target> move <easeTime> <easeType> <easeFunction> <oldPos> <oldYaw> <oldPitch> <oldRoll> <newPos> <newYaw> <newPitch> <newRoll> #(4)!
camera <target> move <easeTime> <easeType> <easeFunction> pos <pos> rot <yaw> <pitch> <roll> #(5)!
camera <target> move <easeTime> <easeType> <easeFunction> pos <pos> #(6)!
camera <target> move <easeTime> <easeType> <easeFunction> rot <yaw> <pitch> <roll> #(7)!
camera <target> clear # (8)!

camera <target> fov set <fov> [easeType] [easeFunction] [easeTime] # (9)!
camera <target> fov set from <oldFov> to <newFov> <easeType> <easeFunction> <easeTime> # (10)!
camera <target> fov clear [easeType] [easeFunction] [easeTime] # (11)!

camera <target> shake set <layer> <type> <intensity> <speed> <duration> [attack] [decay] # (12)!
camera <target> shake set <layer> <type> <intensity> <speed> infinite [attack] [decay] # (13)!
camera <target> shake clear <layer> # (14)!
camera <target> shake clear all # (15)!

hide hud hide [players] # (16)!
hide hud show [players] # (16)!
hide hand hide [players] # (16)!
hide hand show [players] # (16)!

input keyboard lock [players] # (16)!
input keyboard unlock [players] # (16)!
input mouse lock [players] # (16)!
input mouse unlock [players] # (16)!

```

1. Sets the camera's position and rotation to specific values.
2. Sets the camera's position to a specific value.
3. Sets the camera's rotation to specific values.
4. Moves the camera to a new position and rotation over a specified duration with easing options.
5. Moves the camera to a new position and rotation over a specified duration with easing options.
6. Moves the camera to a new position over a specified duration with easing options.
7. Moves the camera to a new rotation over a specified duration with easing options.
8. Clears the camera's current settings.
9. Sets the camera's field of view to a specific value.
10. Changes the camera's field of view from one value to another over a specified duration with easing options.
11. Clears the camera's field of view settings.
12. Sets the camera's shake effect to specific values for a given layer.
13. Sets the camera's shake effect to specific values for a given layer, with an infinite duration.
14. Clears the camera's shake effect for a given layer.
15. Clears all of the camera's shake effects.
16. The players field is optional, if not specified, the command will be executed for the player executing the command.

</div>

## Using the Camera System in Mods

To use the Camera System in your mod, you can call the static methods provided by the `CameraSystem` class.<br>
These methods allow you to control the camera for specific players or groups of players, enabling you to create dynamic and immersive experiences in your mod.
Each of these methods has a variant that takes a single `ServerPlayer` and another that takes a `Collection<ServerPlayer>`, allowing you to target individual players or multiple players at once.

Make sure to check the [CameraManager](https://github.com/GCJOJO/LibLib/blob/1.21.1/common/src/main/java/io/github/gcjojo/liblib/CameraManager.java) class for a complete list of available methods and their usage.

Here is a brief overview of the available methods:

<div class="annotate" markdown>
```java
// Methods for controlling the camera
CameraManager.setCameraPosition(serverPlayer, new Vec3(0, 10, 0));
CameraManager.setCameraRotation(serverPlayer, new Vector3f(0, 90, 0));
CameraManager.setCameraTarget(serverPlayer, new Vec3(0, 10, 0), new Vector3f(0, 90, 0));
CameraManager.setCameraMovement(serverPlayer, new Vec3(0, 10, 0), new Vector3f(0, 90, 0), new Vec3(10, 10, 10), new Vector3f(0, 180, 0), Easing.LINEAR, 2.0f);
CameraManager.clearCamera(serverPlayer);

CameraManager.setFov(serverPlayer, 90.0);
CameraManager.setFov(serverPlayer, 70.0, Easing.LINEAR, 1.0f);
CameraManager.clearFov(serverPlayer);
CameraManager.clearFov(serverPlayer, Easing.LINEAR, 0);

// Methods for shaking the camera
CameraManager.shake(serverPlayer, 0, CommandHelpers.ShakeType.POSITIVE, 1.0f, 1.0f, 1.0f, 1.0f, 1.0f);
CameraManager.clearShake(serverPlayer, 0);
CameraManager.clearAllShake(serverPlayer);

// Methods for hiding HUD elements
CameraManager.hideHud(serverPlayer, LibLibNetwork.HideHudPayload.HideHudElement.HUD, true);
CameraManager.hideHud(serverPlayer, LibLibNetwork.HideHudPayload.HideHudElement.HAND, false);

```
</div>