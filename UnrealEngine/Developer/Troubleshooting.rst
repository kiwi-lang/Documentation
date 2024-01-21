Troubleshooting
===============

* GameplayCues are not playing:
    * Make sure the GameplayTag for each cues exist
    * Make sure the GameplayCue lookup path is set correctly
    * Recompile each gamecue to force the engine to pick them up

* Cooldowns are not blocking:
    * Make sure the GameplayTag are setup
    * Recompile each Abilities to force the engine to pick them up

* Gamekit Content is not found during cooking
    * Make sure Gamekit Engine version match the engine version you are using; UAT skip mouting content folder that have mismatched engine versions.

* Input are not responding:
    * Make sure enhanced input plugin is enabled
    * Make sure project config use enhanced input Component class as default
        * Default Player Input Class: EnhancedPlayerInput
        * Default Input Component Class: EnhancedInputComponent

* Materials are defaulting to UE placeholder
    * Recompile shaders
    * Make sure the constructor sets the Materials
    * For decals it is better to call its own CreateDynamicMaterial method than the Blueprint callable.

* Experience & Levels are not updated
    * Make sure the experience datatable is set in the project settings (``Project > Plugin > Gamekit > Experience Data Table``)
    * Restart the editor

* Actor Target abilities are not able to acquire a valid target or the target is marked as invalid
    * make sure the team table is set in the project settings (``Project > Plugin > Gamekit > Team Table``)
    * Restart the editor

* Path finding is not working on movement abilities:
    * Log shows: ``LogGKNav: Error: No NavSystem found``
    * Make sure you have a ``NavMeshBoundsVolume`` in your level
    * Delete ``RecastNavMesh-Default`` in your level to force its regeneration
    * For multiplayer games; make sure you enabled client side navigation

* Pawn is not rotating toward movement
    * Character Movement Component > Orient Rotation To Movement ``[x]``
    * Pawn Class Defaults > Use Controller Rotation > ``[ ]`` Pitch, ``[ ]`` Yaw  ``[ ]`` Roll

* Unreal Engien crash because of `Assertion failed: !bInitializedSerializationHistory`
    * Your platform was not whitelisted by Gamekit
    * To enable it regardless you can add you platform name inside `Gamekit.uplugin`


.. comment:

    [Core.System]
    Paths=%GAMEDIR%Content/../Plugins/Content