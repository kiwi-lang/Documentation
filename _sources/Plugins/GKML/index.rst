Machine Learning
================

* Tag: |GKML_tag|
* Identifier: |GKML_identifier|
* Commit: |GKML_commit|

.. image:: https://readthedocs.org/projects/cartpole/badge/?version=latest
   :target: https://delaunay.github.io/GKMachineLearning/
   :alt: Documentation Status

UE5 plugin providing tools for machine learning.
This plugin documents how to use the MLAdapter plugin for machine learning
by reimplementing the Cartpole environment.

.. image:: /_static/ML/Cartpole_big.png


Requirements
~~~~~~~~~~~~

* UE4 - 5.0+

.. note::

   For UE5 on linux you will need to disable 2 plugins (XGEController and FastBuildController as of Jan 2022)


Packaged Install
~~~~~~~~~~~~~~~~

Unfortunately U4ML python package is not open source and you will need to
create an Epic account to install it on your machine.
Once it is install you can run any packaged environment without installing or compiling UnrealEngine.

.. code-block:: bash

   # Install MLAdapter python package
   python -e UnrealEngine/Engine/Plugins/AI/MLAdapter/Source/python

   # Download the GKML environment
   wget
   pip install cartpole-0.0.0-py3-none-any.whl

   # run the packaged environment for training
   cartpole-train --launch


Development Install
~~~~~~~~~~~~~~~~~~~

.. note::

   This repo started using UE5 after commit ``332ae357235995d1184effdb060``


Install the python package to run this example as a gym environment

.. code-block:: bash

   git submodule add https://github.com/Delaunay/GKMachineLearning Plugins/GKML
   pip install -e Plugins/GKML

   # Install MLAdapter python package
   python -e UnrealEngine/Engine/Plugins/AI/MLAdapter/Source/python

   # this will compile the project
   UnrealEditor MyProject.uproject

   # Click play in the editor to start the game

   # this will connect to the game running inside the editor
   cartpole-train --no-launch


To run the example just launch the appropriate script

.. code-block:: bash

   python Source/python/cartpole/run.py --project E:/cartpole/Cartpole.uproject --exec E:/UnrealEngine/Engine/Binaries/Win64/UE4Editor.exe


Making of Cartpole
~~~~~~~~~~~~~~~~~~

.. toctree::
   :maxdepth: 1

   cartpole/1_Introduction
   cartpole/2_Setup
   cartpole/3_MLAdapter
   cartpole/4_Game
   cartpole/5_Launching
   cartpole/6_Training
   cartpole/7_Packaging


Developer
~~~~~~~~~

.. toctree::
   :maxdepth: 1

   issues
   api/cartpole
   python/index
