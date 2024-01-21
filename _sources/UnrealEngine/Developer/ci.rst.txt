Continuous Integration
======================

You can setup a CI using github actions.
Epic Games release UnrealEngine containers you can use if you are authenticated.
You will need to use the slim version as the regular version is too big and will not download.

.. warning::

   Using the free runner provided by github is extremely slow.
   Cooking a simple project can take up to 3h.
   The runner has only 2 cpus and 500 Mo of RAM.


.. note::

   Resources on the github action worker is limited.
   You might need to consider `self-hosting it <https://docs.github.com/en/actions/hosting-your-own-runners/about-self-hosted-runners>`_.
   If your project is open source you need to be cautious about its running policy
   as it might be configured to run arbitrary code from any contributors.


Gitlab Runner
-------------


Windows
^^^^^^^


Linux
^^^^^

.. code-block:: bash

   sudo curl -L --output gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64

   sudo chmod +x gitlab-runner

   sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash

   # Remove logout script
   sudo su gitlab-runner
   mv ~/.bash_logout ~/.bash_logout.bak
   exit

   # Create the build directory
   mkdir -p /opt/runner/bulds
   chown ./gitlab-runner:gitlab-runner /opt/runner/bulds

   # Setup the runner
   sudo ./gitlab-runner install --user=gitlab-runner --working-directory=/opt/runner
   sudo ./gitlab-runner start
   sudo ./gitlab-runner register --url https://gitlab.com/ --registration-token $REGISTRATION_TOKEN


.. note::

   if you are using directory with different kind of owner you will need
   `git config --global --add safe.directory /opt/Projects/GamekitDev/Plugins/Gamekit`


.. note::

   You can crosscompile to Linux from windows, but you will be able to run
   the compiled version. (Maybe WSL could be setup to make it work)


.. note::

   When it comes to running the editor Linux is slower than windows.


Github Actions
--------------

.. code-block:: yaml

   name: tests

   on: [push]

   # see https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Containers/ContainersQuickStart/
   jobs:
   cooking:
      runs-on: ubuntu-latest
      container:
         image: ghcr.io/epicgames/unreal-engine:dev-slim-4.27
         credentials:
         username: ${{ github.actor }}
         password: ${{ secrets.CONTAINER_REGISTRY_PAT }}

         # Github expects us to be root, not ue4
         # ue4 wont be able to write anything anywhere
         # NB: Cooking refuse to work as root
         options: "-u root"

      steps:
         - name: Update Git
           run: |
             sudo add-apt-repository ppa:git-core/ppa -y
             sudo apt-get update
             sudo apt-get install git -y
             git --version

         - uses: actions/checkout@v2
           with:
           submodules: true

         - name: Cook
           run: |
             # Paths need to be absolute or they are considered relative to the Engine
             export PROJECT="$(pwd)/Chessy.uproject"
             export COOKED="$(pwd)/Cooked"
             export LOGS="$(pwd)/Saved/UAT"

             # As root we can change ownership of everything
             chown -R ue4 $(pwd)

             # Set a writable log location
             export uebp_LogFolder=$LOGS

             # Run as ue4 since it refuses to run as root
             runuser -u ue4 -- /home/ue4/UnrealEngine/Engine/Build/BatchFiles/RunUAT.sh \
               BuildCookRun                                           \
               -unattended                                            \
               -utf8output                                            \
               -platform=Linux                                        \
               -clientconfig=Shipping                                 \
               -serverconfig=Shipping                                 \
               -project=$PROJECT                                      \
               -noP4 -nodebuginfo -allmaps                            \
               -cook -build -stage -prereqs -pak -archive             \
               -archivedirectory=$COOKED

         - name: Upload
           uses: actions/upload-artifact@v2
           with:
             name: cooked-chessy-linux
             path: Cooked/*

.. note::

   ``CONTAINER_REGISTRY_PAT`` is a github personnal access token with read package permission
