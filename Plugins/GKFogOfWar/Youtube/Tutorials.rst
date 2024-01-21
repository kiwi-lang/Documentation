Tutorials
=========


Getting Started
===============


   The plugin provides everything out of the box so you can get started right away
   with minimal amount of setting up.

   Just use the `GKFoW_GameMode`.

* Installation

   Once you are ready to experiment, you can start by inheriting from the plugin own blueprint


   NOTE: you do not need a CPP project to use this but for packaging purposes it is better to use one
   to turn a Blueprint project into a C++ project you can use uetools to do the conversion seamlessly

#. Create a Landscape for the base terrain

#. Create a new GameState

   This hold the team info of the game

#. Tag starting point with the right team


#. Add A fog of War volume



   The volume is used to manage the extent of the fog as well as managing the replication
   of each actors that belong to the fog of war

   #. Configure the Fog of war



      #. Strategy: ShadowCasting
      #. Grid: Square size used to represent the fog 
      #. Transform
         #.  GPU Upscaler Fast
            #. With Smoothing

         # Exploration Transform
            #. Use Upscaled Version
            #. Use Materials
            #. Texture Size

#. Create a new character that inherit from GKFoW_Character
   NOTE: this is important for network games because the underlying implementation in C++
   it what drives the replication and it cannot be done in blueprint

#. Create obstacles that block vision

   Default behaviour is to use the collision bounding box to render the obstacle on the fog of war
   You can use a more precise shape by implementing the FogOfWarAgent interface and provide the collision shape
   to use to render the obstacle

   NOTE: for better result make sure you align your obstacles to the grid

#. Play



Replication
===========

The FogOfWarVolume authority draws the fog of war and use it to determine which character is visible by whom.
If the enemy character is visible it gets replicated. Allies always get replicated.

On the client side only the components that are visible gets replicated and only those components are drawn on the fog
of the client.

This means clients only have a limited amount of information, this is important for competitive games; 
If it was not the case acheater could try to modify the RAM to expose enemies that should be invisible.
In our case the data is not even on the client and the attack would fail.


Performance
===========

* To increase performance you can

   * Increase the Grid Size
   * Decrease the Volume Size
   * Decrease the number of units



Debugging
=========

* To help users see the fog and how to obstacles are drawn on the map,
we can drag `GKFoW_DecalView` which will render the obstacles, vision and exploration texture on different channel.
This can help users detect misconfiguration 

Styling
===============

   Because the fog is replicated and it needs to be drawn on the server we cannot rely on GPU
   to draw the fog, it needs to leverage the CPU alone.

   To make sure the fog is fast has to be drawn and on very low resolution texture.
   If we were to use this texture directly the resutling effect would be very distracting.

   - Show Fog Without Upscaling

   To remediate this shortcoming the low resolution texture undergoes 2 main transformations;
   an 4x upscaling that will smooth out the edges of the fog and temporal smoothing that will 
   soften the transition between frames when the character is moving.

   - Show Fog With Upscaling - Without Smoothing
   - Show Fog With Upscaling & Smoothing

   While it is recommended to use Upscaling with Smothing the original texture is available.

