Fog of War
==========

.. raw:: html

   <iframe width="696" height="391" src="https://www.youtube.com/embed/R84bn8KMARA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


Features
--------

Versatile fog of war implementation;

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
* 128 Height level
* Configurable Fog Resolution
* Examples included
    * Minimap
    * Full Playable demo


Useful Links
------------

* `Marketplace <https://www.unrealengine.com/marketplace/en-US/product/91c97c089e004ac69f8fd37566e8b449>`_
* `Playable demo <https://setepenre.itch.io/gkfogofwar>`_
* `Bug Tracker <https://gitlab.com/mischievousgame/gkfogofwar/-/issues>`_
* `Documentation <https://mischievousgame.gitlab.io/gkfogofwar/>`_
* `Youtube Channel <https://www.youtube.com/@mischievousgame>`_
* `Discord Server <https://discord.gg/eqb4Egv9b3>`_
* `Patreon <https://www.patreon.com/setepenre>`_
* `Twitter <https://twitter.com/SetepenreKit>`_


.. toctree::
   :caption: Welcome

   Welcome/Installations
   Welcome/GettingStarted
   Welcome/FrequentQuestions
   Welcome/Changelog

.. toctree::
   :caption: C++ API

   API/classAGKFogOfWarCharacter.rst 
   API/classAGKFogOfWarGameMode.rst 
   API/classAGKFogOfWarGameState.rst 
   API/classAGKFogOfWarObstacle.rst 
   API/classAGKFogOfWarPawn.rst 
   API/classAGKFogOfWarPlayerController.rst 
   API/classAGKFogOfWarPlayerState.rst 
   API/classAGKFogOfWarPrivatePlayerState.rst 
   API/classAGKFogOfWarTeam.rst 
   API/classAGKFogOfWarVolume.rst 
   API/classFGKFogOfWarModule.rst 
   API/classFGKFogOfWarShaderModule.rst 
   API/classIGKFogOfWarAgentInterface.rst 
   API/classIGKFogOfWarGameStateInterface.rst 
   API/classIGKFogOfWarTestModule.rst
   API/classUGKCanvasUpscaler.rst 
   API/classUGKCPUUpscalerStrategy.rst 
   API/classUGKExplorationTransform.rst 
   API/classUGKFogOfWarComponent.rst 
   API/classUGKFogOfWarLibrary.rst 
   API/classUGKFogOfWarStrategy.rst 
   API/classUGKGPUUpscalerStrategy.rst 
   API/classUGKRayCasting__Less.rst 
   API/classUGKRayCasting__Line.rst 
   API/classUGKRayCasting__Triangle.rst 
   API/classUGKShadowCasting.rst 
   API/classUGKSharedBlueprint.rst 
   API/classUGKTransformerStrategy.rst 
   API/classUGKTransformerStrategyCanvas.rst 
   API/classUGKTransformerStrategyTexture2D.rst


Indices and tables
~~~~~~~~~~~~~~~~~~

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
