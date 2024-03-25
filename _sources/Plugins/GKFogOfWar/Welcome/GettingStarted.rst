Getting Started
===============

This tutorial is available on `youtube <https://www.youtube.com/watch?v=a0FDXMrEktw&list=PLLmwojbdxBrW86-HToVJp29lBvCseTnrl>`_

.. contents:: Table of contents
    :local:
    :backlinks: entry
    :depth: 2


Verify Installation
--------------------

.. raw:: html

   <iframe width="696" height="391" src="https://www.youtube.com/embed/a0FDXMrEktw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


1. Open a new project

2. Make sure Plugin content is visible
      ``Content Drawer / Settings / Show Engine Content [X]``
      ``Content Drawer / Settings / Show Plugins Content [X]``

3. Load Example Map
      ``Plugins / GKFogOfWarContent / Example / FogOfWar``

4. Set Game Mode Override
      ``WorldSettings / GameMode Override / GKFoW_GameMode``


Create your own
---------------

Initial Setup
^^^^^^^^^^^^^

.. raw:: html

   <iframe width="696" height="391" src="https://www.youtube.com/embed/_reODyCUi2c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


1. Create a new Game State from ``GKFoW_GameState`` (inherits from :cpp:class:`AGKFogOfWarGameState`)
      Update the team information if need be
      ``AGKFogOfWarGameState > Teams > Fog Of War Teams``

2. Create a new Game Mode from GKFoW_GameMode (inherits from :cpp:class:`AGKFogOfWarGameMode`)
      Inside GameMode set the game state to the newly created game state

   .. note::

      The game mode is used to initialize the Fog Of War before the game starts.
      You can override ``AssignTeamFor`` to customize how teams are assigned to player controller

3. Set the Game Mode Override
      ``WorldSettings / GameMode Override / GKFoW_GameMode``

4. Tag the player start with the team name the player should be starting as

5. Add a :cpp:class:`AGKFogOfWarVolume` to the scene and make it cover the entire map

   .. note::

      Only one volume can be created per map


   .. warning::

      The fog of war texture size should not be above 2048x2048 px (8192 / 4) IF 
      GPU/CPU upscaling is enabled (it is by default)
      

Add obstacles
^^^^^^^^^^^^^

.. raw:: html

   <iframe width="696" height="391" src="https://www.youtube.com/embed/1x5yEe_h9mc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


1. Create a new Pawn
      - Add a :cpp:class:`UGKFogOfWarComponent`
      - ``UGKFogOfWarComponent > GivesVision [ ]``
      - ``UGKFogOfWarComponent > BlocksVision [X]``
      - Add static mesh

2. Place Pawn on the map

.. note::

   You will want to align the obstacles to the fog of war grid to make the bounds match as closely as possible.
   See `Actor snapping <https://docs.unrealengine.com/4.27/en-US/Basics/Actors/ActorSnapping/>`_.

Add Landscape
^^^^^^^^^^^^^

.. raw:: html

   <iframe width="696" height="391" src="https://www.youtube.com/embed/oYrc49KBD2w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


1. Create a landscape
      Add bumps

2. Add the landscape to the Fog of War Volume
      ``Fog Of War Volume / Strategy / Landscape``

3. Make sure the Fog of war is below the landscape

4. Make sure the Navigation Bound Volume includes the landscape


Custom collision Shapes
^^^^^^^^^^^^^^^^^^^^^^^

.. raw:: html

   <iframe width="696" height="391" src="https://www.youtube.com/embed/ZY6-HwL77MU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


1. Open an Obstacle Pawn

2. Add Box/Sphere/Cylinder Collision Shape

3. Make sure the shape covers the area that blocks visions

4. Implement the ``GKFogOfWarAgentInterface``
      - ``Class Settings / Interfaces / Add /  GKFogOfWarAgentInterfaces``
      - Implement GetFogOfWarComponent by returning the component
      - Implement GetFogOfWarCollisionShape by returning the shape


.. note::

   Only rectangle, yaw rotated rectangle and circle obstacles are supported.


Update Cylinder Obstacles
^^^^^^^^^^^^^^^^^^^^^^^^^

.. raw:: html

   <iframe width="696" height="391" src="https://www.youtube.com/embed/BHUjUqkO5PQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


1. Open an Obstacle Pawn
      - Add Box/Sphere/Cylinder Collision Shape
      - Make sure the shape covers the area that blocks visions
      - ``Class Settings / Interfaces / Add /  GKFogOfWarInterfaces``
      -  Implement GetFogOfWarComponent by returning the component
      - Implement GetFogOfWarCollisionShape by returning the shape


Player Starts
^^^^^^^^^^^^^

.. raw:: html

   <iframe width="696" height="391" src="https://www.youtube.com/embed/nQ0LId6lhQY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


1. Create a Second PlayerStart
      Change the tag to the enemy team (BadGuys)

2. Change the Network mode to Clients
      ``Editor / Change Play Mode / Net Mode / Client``

3. Change the number of players to 2
      ``Editor / Change Play Mode / Number of Players / 2``


.. note::

   You should `enable client side navigation <https://www.youtube.com/watch?v=wd5kt8jNG54>`_ for clients to move correctly.

      ``Project Settings / Engine / Navigation System / Allow Client Side Navigation [X]``


Debugging
^^^^^^^^^

.. raw:: html

   <iframe width="696" height="391" src="https://www.youtube.com/embed/cb0AIyTbJK8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


1. Navigate to
      ``Plugins / GKFogOfWar Content / Debug / GKFoW_DecalView``

2. Drag and drop the decal on the map

3. Scale it to cover the map

4. Enable debug mode on the Fog of War Volume


Disable auto-exposure
^^^^^^^^^^^^^^^^^^^^^

.. raw:: html

   <iframe width="696" height="391" src="https://www.youtube.com/embed/JPqrLzggvRw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


The fog of war will darken your screen, by default UE has auto exposure enabled which can create a 
distracting effect when large area are revealed.

1. Drag a drop a post process volume

2. Disable Auto exposure
      ``Post Process Volume / Exposure / Min Brightness / 1``
      ``Post Process Volume / Exposure / Max Brightness / 1``

3. Make the Post Process Volume unbounded
      ``Post Process Volume  /  Volume Settings / Infinite Extent [X]``


Details
-------

Classes
^^^^^^^

* :cpp:class:`AGKFogOfWarGameState`:
   * implements :cpp:class:`IGKFogOfWarGameStateInterface`
   * provides a list of teams that will participate in the game

* :cpp:class:`AGKFogOfWarGameMode`:
   * extends AGameMode
   * expose new blueprint event ``AssignTeamFor`` used to assign a team to each player controller

* :cpp:class:`AGKFogOfWarPlayerController`:
   * extends the base PlayerController to make it belong a given team; it handles dynamic team change.

* :cpp:class:`AGKFogOfWarCharacter`:
   * extends the base Character
   * implements fog of war conditional replication, it is only replicated to enemies if it is seen by them.

* :cpp:class:`AGKFogOfWarPlayerState`:
   * extends ``APlayerState``
   * expose a new attribute ``AGKFogOfWarPrivatePlayerState`` which is only replicated to allies.

* :cpp:class:`AGKFogOfWarVolume`:
   * Draws the fog of war periodically

* :cpp:class:`UGKFogOfWarComponent`:
   * Register itself to the Fog of War volume
   * Specify how the actor fog of war should behave (blocks light, provide vision, vision radius)

* :cpp:class:`UGKFogOfWarStrategy`:
   * Implements how the fog is drawn

* :cpp:class:`UGKTransformerStrategyCanvas`:
   * Implements material based transformation on the vision texture
   * this is used to implement upscaling and exploration (blending of previous & current vision)


Initialization Flow
^^^^^^^^^^^^^^^^^^

.. image:: /_static/FogOfWar/InitializationFlow.png


Replication Flow
^^^^^^^^^^^^^^^^

.. image:: /_static/FogOfWar/ReplicationFlow.png
