Debugging
=========

For debugging you can render the different layers of the fog of war using a decal.
A blueprint is provided for this exact purpose ``Blueprint'/GKFogOfWar/Debug/GKFoW_DecalView'``

You will need to populate the following fields

* ``AGKFogOfWarVolume > Editor > Debug [X]``

The colors used are:

* Red: Blocking volume
* Green: Active vision
* Blue: Exploration

.. image:: /_static/FogOfWar/DebugView.png


