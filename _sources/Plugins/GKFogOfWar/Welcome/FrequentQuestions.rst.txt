Frequently Asked Questions
==========================

.. contents:: Table of contents
    :local:
    :backlinks: entry
    :depth: 2


Destroyed obstacle persist on the navmesh
*****************************************

* Project Settings -> Navigation Mesh -> Runtime -> Runtime Generation -> Dynamic

Missing Fog of War Plugin on shipping builds
********************************************

* Make sure your base project has a C++ module
* You can use `uetools <https://github.com/kiwi-lang/uetools>`_ to transform a blueprint project to a C++ one
* ``uecli cpp --project <MyProjectName>``


After spawning a few 100 units my FPS drops
*******************************************

* UE meshes and animations are often overkill for RTS and hog a lot of performance
* UE movement component is slow and quite expensive
* Profile your game to find the bottleneck
    * Using unreal console start profile ``stat startfile`` and let it run for 1 minute, then stop "stat stopfile".
    * It will generate a file inside ``GKFogOfWarDemo_Win64\GKFogOfWarDemo\Saved\Profiling\UnrealStats\FogOfWar-Windows-01.05-10.17.55``
    * Open the profile with the UnrealEditor to see what took time ``Tools > Session FrontEnd > Profiler > Load`
    * Select the Game Thread and you will be able to see something like below


.. image:: /_static/FAQ/GKFogOfWar_Profiling.PNG


Disable exploration
*******************

* You can disable the Exploration directly by simply removing the Exploration transform in the GKFogOfWarVolume;
    that way no GPU time is wasted on the exploration.

    ``GKFogOfWarVolume > Fog Of War > Transform > Exploration > None``

Increase performance
********************

* Decrease vision radius size

    ``GKFogOfWarComponent > Fog of War > Radius``

* Increase FogOfWarVolume Grid Size

    ``GKFogOfWarVolume > Fog Of War > Grid > (X, Y)``

Create Pawn with an assigned Team without player start
*****************************************

* You need to implement the ``IGenericTeamAgentInterface`` that is built in UnrealEngine
* You can use ``GKFogOfWarChararacter`` which implements the interface as base;

Can you create an actor that is visible on both teams ?
*****************************************

* This is not possible, You can overlay the actor with a dummy actor for each time to give them vision

I only want heroes to have vision, and not shared with their allies is that possible ?
**************************************************************************************

* You can do that by creating a team for each hero 
* Inside the Fog of War Volume set ``AGKFogOfWarVolume::VisionSharingSetting`` to ``UseBoth``. 
  This configure the Volume to use a separate system for vision sharing and TeamAttitude.
  i.e Teams can be friendly without `sharing visions <https://mischievousgame.gitlab.io/gkfogofwar/Welcome/Changelog.html#id1>`_

Can we also make allied units not replicating when invisible ? 
**************************************************************

* Replication is driven by vision first by default; you can use ``AGKFogOfWarVolume::VisionSharingSetting = UseBoth`` 
  to decouple team attitude and vision sharing.
      
Are hp bars (widgets) visible in the fog or not ?
*****************************************

* The HP bars shouldn't be visible in the fog if they are tied to the AActor
* You can use the ``AGKFogOfWarCharacter::OnVisilityChanged`` event to control how the AActor should display on the clients.

Can you save out the explored region of the fog of war and load it back in later?
*****************************************

* The explored region of the fog of war is just a texture. it is created at runtime 
  but you could copy it to a permanent texture or save it inside the game state to load for later

What are the limits of the fog of war in terms of map size ?
************************************************************

* The fog of war is drawn on a texture, unreal engine texture size limit is 8192 (keep in mind that by default the texture is upscaled 4x),
  so the limit is more around 2048. The map size given the texture will be 2048 * GridSize that you choose.
  As an example League of Legend and Dota2 use grid sizes of ~128 units so the max map size would be around 262144 x 262144 units in this case.


For a game where the map is gigantic
************************************

* You can attach the fog of war to your main actor so it follows the actor around, 
  the areas not covered by the fog volume will be dark
* Only one fog of war per map is supported right now.

Do you plan to put the plugin on sale in the future ? 
*****************************************************

* I am not sure how sales work on Epic, if it can advertise and such, for now there are no plans for sales
    

Packaging issue
****************

.. code-block:: bash

    Missing precompiled manifest for 'GKFogOfWar', 'D:\UE_5.1\Engine\Plugins\Marketplace\GKFogOfWar\Intermediate\Build\Win64\UnrealGame\Shipping\GKFogOfWar\GKFogOfWar.precompiled'. This module was most likely not flagged for being included in a precompiled build - set 'PrecompileForTargets = PrecompileTargetsType.Any;' in GKFogOfWar.build.cs to override. If part of a plugin, also check if its 'Type' is correct.

* This is a recurring problem for other plugins
* The only solution right now is to copy the plugin to the project folder


Where do we adjust the fog color ?
**********************************

* I want to make the unexplored areas of the map fully black 
    * You can create a new instance of the FogOfWarPostProcess material and tweak the values inside.
      Do not forget to update the Fog of War volume to use the newly created material instance.



Combining Plugins/Assets
************************

* Can I use this asset in conjunction with another plug-in which may have its own GameMode, etc?
  * Yes, you can, the GameMode and other provided classes are only examples.
    You can create your own. The FogOfWar use the interface system to extend GameMode and other classes.
    You simply need to implement the interfaces in your own custom GameMode to make them comptabile



Characters_0/Controller_0 get assigned to different teams on clients
*********************************************************************

* The Characters_0 and Controller_0 are always the client main character/controller.
  that is why they get assigned to different teams.

Sometimes when coming out of the fog, the unit slides from the position it entered the fog to its actual position
*****************************************************************************************************************

* This is how UE handles the resume replication on the movement side,
  it will do a linear interpolate to smooth out the transition.
  The movement code is not really tuned for RTS games.
  You can tweak the Chracter Movement Component > Networking > No Smooth Update Distance  and set it to something small
  to prevent smoothing when the character is far away.

Only Yaw Rotation is handled
****************************

* I get a warning about `Only Yaw Rotation is handled`
  * An obstacle object has an x or y rotation but only the z rotation is taken into account when drawing the obstacle.


The fog of war is not centered
******************************

* Make sure your fog of war volume is scaled uniformly and that the grid has the same size on the x and y axis.


Linking Error
*************

.. code-block:: bash

    MyGKFogOfWarCharacter.gen.cpp.obj : error LNK2001: symbole externe non résolu "public: virtual enum ETeamAttitude::Type cdecl IGenericTeamAgentInterface::GetTeamAttitudeTowards(class AActor const &)const " (?GetTeamAttitudeTowards@IGenericTeamAgentInterface@@UEBA?AW4Type@ETeamAttitude@@AEBVAActor@@@Z)
    MyGKFOWCharacter.gen.cpp.obj : error LNK2001: symbole externe non résolu "public: virtual enum ETeamAttitude::Type cdecl IGenericTeamAgentInterface::GetTeamAttitudeTowards(class AActor const &)const " (?GetTeamAttitudeTowards@IGenericTeamAgentInterface@@UEBA?AW4Type@ETeamAttitude@@AEBVAActor@@@Z)
    MyGKFogOfWarCharacter.cpp.obj : error LNK2001: symbole externe non résolu "public: virtual enum ETeamAttitude::Type cdecl IGenericTeamAgentInterface::GetTeamAttitudeTowards(class AActor const &)const " (?GetTeamAttitudeTowards@IGenericTeamAgentInterface@@UEBA?AW4Type@ETeamAttitude@@AEBVAActor@@@Z)
    MyGKFOWCharacter.cpp.obj : error LNK2001: symbole externe non résolu "public: virtual enum ETeamAttitude::Type cdecl IGenericTeamAgentInterface::GetTeamAttitudeTowards(class AActor const &)const " (?GetTeamAttitudeTowards@IGenericTeamAgentInterface@@UEBA?AW4Type@ETeamAttitude@@AEBVAActor@@@Z)
    D:\UE_Projects\GKFOG_TEST_03\Binaries\Win64\UnrealEditor-GKFOG_TEST_03.patch_0.exe : fatal error LNK1120: 1 externes non résolus
    Failed to link patch (0.000s) (Exit code: 0x460)
    ---------- Finished (0.000s) ----------

* Linking errors usually means a dependency is missing
* Update your game modules to include the following modules ``AIModule``, ``Landscape``, ``RenderCore``, ``RHI``


LogLinker Warning
*****************

.. code-block:: bash

  LogLinker: Warning: [AssetLog] C:\Documents\Unreal\FPTemplate 5.1\Plugins\GKFogOfWar\Content\Upscaling\MT_Upscaling.uasset: Asset has been saved with empty engine version. The asset will be loaded but may be incompatible.

> This warning exists to warn when engineers who are working with local changes save assets that may not be compatible with your team's "promoted" build.
> Probably 95% of the time even in large teams, it is benign and if you are a developer who is working on their own pretty much guaranteed to be ignorable.
> It can be disabled in DefaultEngine.ini by adding if you are certain you don't need it (at least one of internal game teams do have it disabled):

To Disable the warning the the lines below inside ``DefaultEngine.ini``

.. code-block:: ini

   [Core.System]
   ZeroEngineVersionWarning=False
