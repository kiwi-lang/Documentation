Release Procedure
-----------------


* Tag new version


.. code-block:: bash

   git tag v...
   git push origin maste v...
   uecli gitversion --file E:\GamekitDev\Plugins\GKFogOfWar\Source\GKFogOfWar\GKFogOfWar.Build.cs --namespace GKFOGOFWAR


* Compile to the Demo Project

.. code-block:: bash

   uecli plugin GKFogOfWar.uplugin --output E:/GKFogOfWarDemo/Plugins/GKFogOfWar --platforms Win64


* Compile Release 

.. code-block::

   uecli plugin GKFogOfWar.uplugin --output E:/Temporary/GKFogOfWar --platforms Win64


* Compile Demo

.. code-block::

   uecli uat-cook --project GKFogOfWarDemo --platform Win64 --clientconfig Development --archivedirectory E:/Temporary/GKFogOfWarDemo


* Copy Config from Plugin to release
* Delete binaries from release


* Update itch.io demo
* Update marketplace plugin
