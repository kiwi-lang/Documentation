Changelog
=========

01/12/2022 - v1
---------------

Features
^^^^^^^^

* Fully Replicated
    * Conditional Replication for clients: Enemy actors are only replicated if it is visible
    * Cheat prevention: clients do not know about enemy actors until visible
   
* Dynamic
    * Faction change
    * Obstacle
    * Unlimited Number of Teams
   
* Fast C++ Implementation
    * Multithreaded
    * Fully exposed to blueprints
    * Fully extendable in C++ and Blueprints
   
* Up to 64 Teams
* 128 Height level
* Configurable Fog Resolution
* Examples included
    * Minimap
    * Full Playable demo


15/01/2023 - v1.2
-----------------

Features
^^^^^^^^

* Allow teams to share vision [#8]
   * Vision sharing can be controlled in different ways (Use ``AGKFogOfWarVolume::VisionSharingSetting`` to configure):
      * UseGenericTeamSolver (Old Behavior): 
         * we use unreal engine builtin ``FGenericTeamId::GetAttitude()``
         * If Teams are Friendly then vision is shared 
      * UseFogOfwarTeamSolver (new default):  
         * we use Fog of War internal solver that will replace the default attitude solver used by ``FGenericTeamId``
         * Authority can control which team is visible by which using ``AGKFogOfWarVolume::SetShareVisibility``.
         * Teams that share vision with another become ally (i.e ``FGenericTeamId::GetAttitude()`` will return Friendly).
         * Vision sharing does not have to be symmetric.
         * You need to call ``SetShareVisibility(A, B, true)`` and ``SetShareVisibility(B, A, true)`` to make it symmetric.
      * UseBoth:
         * Both above systems are used separately
         * Friendly teams do not need to share vision and enemy teams could share vision.
         * Calling ``AGKFogOfWarVolume::SetShareVisibility`` only change visibility and has no impact of the Team attitude.
   * Use ``WITH_GENERICTEAMSOLVER=1`` so force **UseGenericTeamSolver** at compile time
  
* Team Vision Caching (Authority Only)
   * If vision sharing is reciprocal (i.e if Team A shares its vision with B and B share its vision with A)
     then the vision texture are the same and TeamB vision drawing can be skipped and use TeamA texture instead
   * Can be disabled at runtime with ``bCacheSimilarAllyVision`` inside the FogOfWarVolume
   * Can be disabled at compile time with ``WITH_TEAMCACHING=0``
  
* OnSighted/OnOutOfSight Events (Authority Only) [#11] 
   * Runtime Toggle: ``bBroadcastSightingEvents`` inside the FogOfWarVolume
   * Compile Time Toggle: ``WITH_SIGHTING=0``
  
* Flying units
   * Can be disabled at compile time with ``WITH_FLYINGUNITS=0``
   * Without flying units:
      * Only the obstacles heights are taken into accounts.
      * Vision height is not kept after the initial vision computation.
   * With flying units
       * the unit above sees everything below units below see nothing above
   * NOTE: in practice most RTS do not have true flying units, i.e ground units
     will see flying units.
   * Disabled by default 
     
  
* Allow server to tick at a different speed than clients [#9]
   * By default dedicated server only run at 30 tick per second.
  
Bug Fixes
^^^^^^^^^

* Fix Team color [#10]
* Fix replication issue were clients had characters left as visible after server paused the replication.


15/06/2023 - v1.3
-----------------

* UE 5.2 update


15/10/2023 - v1.4
-----------------

* UE 5.3 update
