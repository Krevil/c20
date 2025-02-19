```.alert info
This is an article about the legacy Sapien for use with [Halo: Custom Edition][h1], for the H1A Sapien for MCC see [H1A Sapien][h1a-sapien]
```
**Sapien**, part of the [HEK][], is a visual [scenario][] and
[BSP][scenario_structure_bsp] editor used to populate levels with objects,
configure BSP [cluster data][scenario_structure_bsp#clusters-and-cluster-data] like wind and sound environments, compile [scripts][scripting], and more. Sapien shares some systems with Halo itself, including its AI system to support interactive AI scripting and debugging. Other systems, such as weather rendering, are not represented.

It is roughly analagous to Forge found in later Halo titles, although the user cannot interact with the world as a player. Users primarily interact with Sapien's windows and menus, but the _Game Window_ also includes a scripting console which supports many more debug commands than the in-game one.

# Menu options
## Switch BSP
It is common for singleplayer scenarios to be comprised of multiple [BSPs][scenario_structure_bsp]. The _Edit > Switch BSP_ option is used to change between them. **Always use this option to switch BSPs** and don't use [`switch_bsp`][scripting#functions-switch-bsp] in the [console][developer-console]. The menu option performs additional functions that maintain proper editor state, whereas `switch_bsp` is intended for level scripts.

# Windows
## Game window
The game window is the main interface when interacting with objects in the level. It is also where you can run commands by pressing the <kbd>~</kbd> (tilde) key. The resolution and aspect ratio cannot be adjusted.

Movement of the camera is done in the same way as the in-game debug camera; **hold the middle mouse button** plus:

* Use the mouse to aim
* Move with <kbd>W</kbd>, <kbd>A</kbd>, <kbd>S</kbd>, and <kbd>D</kbd>
* Go up with <kbd>R</kbd> and down with <kbd>F</kbd>
* Increase camera speed by scrolling down or pressing <kbd>Shift</kbd>
* Decrease camera speed by scrolling up

Camera rotation with the <kbd>G</kbd> key is only supported in-game and not in Sapien.

## Hierarchy view
The Hierarchy view displays all the objects currently placed in the game and organizes them by type. The left pane of the window shows the Hierarchy tree and currently selected type, and the right pane shows the objects of this selected group or type that are currently placed in the level.

## Tool window
This window contains settings for the currently active tool mode, such as object placement, detail object painting, or cluster properties application. The currently active tool depends on the selected hierarchy view item.

The most commonly used settings, or options that are modified the most, are the options under the _Active marker handles_ section and the _Don't draw center marker_ option.

## Properties palette
The Properties palette window displays the properties for the currently selected hierarchy item. The type of object can be changed or chosen in this display as well as various other properties such as the position and rotation of the object, and spawn flags that set various attributes for the object.

When applying cluster properties, the camera location in the game window determines the active cluster shown in this window.

## Output window
This window is unused and can be ignored.

# Keyboard shortcuts/hotkeys
Some of these shortcuts are only used in certain windows or editor modes.

## General
* <kbd>~</kbd>: Opens the command console.
* <kbd>Space</kbd>: clones the selected object to the camera's location and orientation. If multiple objects are selected, uses the first.
* <kbd>Pause/Break</kbd>: Pauses your Sapien instance. Press "OK" in the opened window to resume Sapien.
* <kbd>Control + B</kbd>: Open the BSP switch dialog window.
* <kbd>Control + Shift + B</kbd>: Creates the file `baggage.txt`. If you end up getting a maximum tag slots error or are [running low on tag space][map#limits], this file shows the memory usage of tags in the editor.
* <kbd>Shift + Click</kbd>: Select a group of objects or keep previously placed objects selected. You can also use it to select the first and last object in the hierarchy list to select everything in-between at once. Useful for deleting multiple objects or moving them all at once.
* <kbd>Control + Click</kbd>: Select a group of objects or keep previously placed objects selected. This will only select the object you specifically click in the hierarchy list. Useful for deleting multiple objects or moving them all at once.
* Hold <kbd>Tab</kbd>: Using this key combo while having an object selected will set the rotation gizmo to sync with the local rotation of the object. Only really useful if "Local Axes" is not enabled.
* In the hierarchy view, pressing a key will cycle through all folders that start with that character. For example, pressing <kbd>A</kbd> while having the "Missions" folder expanded will immediately take you to the "AI" folder.
* <kbd>N</kbd>: This hotkey will snap a selected object to the normal of the ground below it. **This hotkey is broken in the Gearbox HEK release and can cause Sapien to crash when restarted. Do not use it!** It also causes editor icons and name overlays to disappear for the session. This issue is fixed in [H1A Sapien][h1a-sapien].

## Encounters and AI
* <kbd>Middle mouse + F1</kbd>: Selects the spawned actor in the center of the game view.
* <kbd>Middle mouse + F2</kbd> Select next encounter. You can also use the console command `ai_select <encounter>`.
* <kbd>Middle mouse + F3</kbd>: Select previous encounter.
* <kbd>Middle mouse + F4</kbd>: When an encounter is selected, selects the next actor.
* <kbd>Middle mouse + Shift + F4</kbd>: Selects the previous actor.
* <kbd>Middle mouse + F5</kbd>: Cycles through render modes for actor sprays:
  * Actions
  * Activation status
  * None
* <kbd>Middle mouse + F6</kbd>: Erase all _spawned_ actors, e.g. those created with `ai_place`.
* <kbd>M</kbd>: Toggles group labels on [firing positions][ai#firing-positions], shows the default actor for move positions used by a squad instance, and highlights [editor gizmos/placeholders][placeholder], making them easier to see.

## Recorded animations
These hotkeys apply in scripted camera mode.

* <kbd>A</kbd>: Toggle "Attach camera to unit" option.
* <kbd>E</kbd>: Toggle "Edit camera point" option.
* <kbd>C</kbd>: Toggle "Scripted camera control".
* <kbd>Space</kbd>: Creates a new camera point at the game view camera's location if "Edit camera point" is disabled. If "Edit camera point" is enabled then it instead moves the "Active camera point" to the camera's location.
* <kbd>Shift + V</kbd>: Using this key combo while in scripted camera mode will take over (posess) the selected unit.
* <kbd>Backspace</kbd>: Cycles through camera types for the posessed unit:
  * First person
  * Third person
  * Flycam
* <kbd>Caps lock</kbd>: Start/stop animation recording. Unfortunately it is not possible to control the posessed unit while recording.
* <kbd>Shift + Q</kbd>: Exits a posessed unit while in scripted camera mode.

See main page: [recorded-animations][]

## Detail objects painting
* <kbd>Shift + Right Click</kbd>: Erases all detail objects in a highlighted cell.
* <kbd>Shift + Control + Right Click</kbd>: As above, but also deleted the cell itself.
* <kbd>Shift + Control + L</kbd>: Relight detail objects (useful after updating [lightmaps][]).

# Radiosity
Both Tool and Sapien can be used to generate [lightmaps][]. To use Sapien, enter the following console commands:

```console
;0 for low quality, 1 for high, or a value like 0.8
radiosity_quality 1
;begins radiosity. numbers will start to count down
radiosity_start
;wait for the numbers to count down to 0 or near 0, then:
radiosity_save
```

If you want progress feedback updated more frequently, you can set `radiosity_step_count 1`. See [Tool's lightmaps documentation][tool#lightmaps] for an explanation of the `radiosity_quality` value. Using [LM_Tool][] is recommended for high quality lightmaps since it is easier to control the stop parameter (when to save) and is faster than using Sapien or Tool.

# editor_init.txt
At startup, Sapien will load `editor_init.txt` if present in the same folder. This file can contain [console commands][developer-console], one per line, which are executed automatically for you. For example:

```inittxt
sound_enable 0
debug_objects 1
;a comment
```

# Compatibility
Windows users have experienced saving issues related to the Virtual Store. Ensure you have the [right permissions][tips#windows-virtual-store] before editing tags.

On Linux, Sapien can be run successfully using [Wine][] but is not yet compatible with [DXVK][]. Use built-in or standard native DirectX libraries instead.

# Limits
As an older 32-bit Windows application, Sapien is limited to 2 GB of virtual memory even on modern 64-bit Windows systems for compatibility. While this memory limit is usually not an issue, an abundance of large textures and other large assets in a map may cause Sapien to crash. To work around this, `sapien.exe` can be patched to tell the OS it supports 4 GB of virtual memory (large address aware, or LAA) using a utility like [NTCore][ntcore]. To do this:

* Install [NTCore 4GB Patch](https://ntcore.com/?page_id=371)
* Run the 4GB Patch.
* Select the Sapien executable.
* NTCore will apply the patch. After it's finished, press OK. Sapien has now been patched to support 4 GB of virtual memory.

[H1A Sapien][h1a-sapien] is already LAA.

[wine]: https://www.winehq.org/
[dxvk]: https://github.com/doitsujin/dxvk
[ntcore]: https://ntcore.com/?page_id=371

# Troubleshooting
## Interface
<table>
  <thead>
    <tr>
      <th style="width:50%">Issue</th>
      <th style="width:50%">Solution</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>The game window is completely black and does not display the console when <kbd>~</kbd> (tilde) is pressed.</td>
      <td>

Sapien, like Halo, does not support [MSAA][msaa]. Add Sapien as a program in your graphics control panel and disable anti-aliasing for it. Fixed in [H1A Sapien][h1a-sapien]
      </td>
    </tr>
    <tr>
      <td>The "edit types" window does not allow tags to be added.</td>
      <td>Unknown. Potential issue with Windows compatibility modes. Try running without a compatibility mode.</td>
    </tr>
    <tr>
      <td>Child windows are not visible or stuck outside the main window.</td>
      <td>
        <p>Open the registry key <code>HKEY_USERS\S-1-5-21-0-0-0-1000\Software\Microsoft\Microsoft Games\Halo HEK\sapien</code> (user ID may vary) using regedit and delete all entries ending with "rect".</p>
      </td>
    </tr>
    <tr>
      <td>
        Sapien debug wireframe colors and bounding radii change at angles and turn black, making it hard to identify their types.
      </td>
      <td>None known for Gearbox Sapien, fixed in [H1A Sapien][h1a-sapien] </td>
    </tr>
  </tbody>
</table>

## Crashes
When Sapien crashes, check `debug.txt` for hints. You can ignore `Couldn't read map file './sapienbeta.map'`.

```.table
dataSource: crashes.yml
dataPath: crashes
wrapPre: true
columns:
  - key: error
    name: Error
    style: "width:50%"
    format: codeblock
  - key: solution
    name: Solution
    style: "width:50%"
    format: text
```


[msaa]: https://en.wikipedia.org/wiki/Multisample_anti-aliasing
