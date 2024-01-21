Installations
=============

GK Fog of War is a project plugin, it can be added to your project easily without overlapping with your own files


From the marketplace
--------------------

1. Click on add to project


.. note::

   The plugin is installed inside ``UE_5.X/Engine/Plugins/Marketplace/GKFogOfWar``


From Source
-----------


1. Simply add the plugin as a git submodule.
2. Regenerate the project solution and compile it
3. Enable the plugin using the editor

.. code-block:: bash

   git submodule add git@gitlab.com:Delaunay/gkfogofwar.git Plugins/GKFogOfWar



.. note::

   GKFogOfWar supports 3 installation locations:

   * Marketplace: ``UE_5.X/Engine/Plugins/Marketplace/GKFogOfWar``
   * Engine: ``UE_5.X/Engine/Plugins/GKFogOfWar``
   * Project: ``<Project>/Plugins/GKFogOfWar``
