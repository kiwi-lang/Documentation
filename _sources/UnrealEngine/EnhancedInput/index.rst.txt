Enhanced Input
==============

Advantages:

* Reusable Input Set
* Context Specific Inputs
* Takes away input logic out of the Controller/Pawn which can focus on the actual gameplay


Triggers
--------

* UInputTriggerDown

Triggered on Press, keeps firing when down

+----------+--------+-----------+--------+---------+-----------+
| Trigger  | Events | Name      | Action | Elapsed | Triggered |
+----------+--------+-----------+--------+---------+-----------+
|   Down   | 1      | Started   | true   | 0.01    | 0.01      |
|          +--------+-----------+--------+---------+-----------+
|          | 2      | Triggered | true   | 0.02    | 0.02      |
|          +--------+-----------+--------+---------+-----------+
|          |              Repeating until release              |
|          +--------+-----------+--------+---------+-----------+
|          | n      | Triggered | true   | 0.03    | 0.03      |
|          +--------+-----------+--------+---------+-----------+
|          | n + 1  | Completed | false  | 0.03    | 0.03      |
+----------+--------+-----------+--------+---------+-----------+


* UInputTriggerPressed

Triggered on press, ignore, down and release event

+----------+--------+-----------+--------+---------+-----------+
| Trigger  | Events | Name      | Action | Elapsed | Triggered |
+----------+--------+-----------+--------+---------+-----------+
| Pressed  | 1      | Triggered | true   | 0.01    | 0.01      |
|          +--------+-----------+--------+---------+-----------+
|          | 2      | Started   | true   | 0.01    | 0.01      |
|          +--------+-----------+--------+---------+-----------+
|          | 3      | Completed | false  | 0.01    | 0.01      |
+----------+--------+-----------+--------+---------+-----------+


* UInputTriggerReleased

Triggered on release, broadcast `Started` on press and `Ongoing` until release

+----------+--------+-----------+--------+---------+-----------+
| Trigger  | Events | Name      | Action | Elapsed | Triggered |
+----------+--------+-----------+--------+---------+-----------+
| Released |  1     | Started   | false  | 0.01    | 0         |
|          +--------+-----------+--------+---------+-----------+
|          |  2     | OnGoing   | false  | 0.02    | 0         |
|          +--------+-----------+--------+---------+-----------+
|          |          Repeating until release                  |
|          +--------+-----------+--------+---------+-----------+
|          | n - 1  | OnGoing   | false  | 0.03    | 0         |
|          +--------+-----------+--------+---------+-----------+
|          | n      | Triggered | false  | 0.04    | 0.01      |
|          +--------+-----------+--------+---------+-----------+
|          | n + 1  | Completed | false  | 0.04    | 0.01      |
+----------+--------+-----------+--------+---------+-----------+


* UInputTriggerChordAction


Timed Triggers
^^^^^^^^^^^^^^

* UInputTriggerHold

Triggered after the input has been pressed for a given amount of time.
broadcast `Started` on press, then `Ongoing` until the threshold time is met,
then `Triggered` until release.

+----------+--------+-----------+--------+---------+-----------+
| Trigger  | Events | Name      | Action | Elapsed | Triggered |
+----------+--------+-----------+--------+---------+-----------+
| Hold     |  1     | Started   | false  | 0.01    | 0         |
|          +--------+-----------+--------+---------+-----------+
|          |  2     | OnGoing   | false  | 0.02    | 0         |
|          +--------+-----------+--------+---------+-----------+
|          |    Repeating until time threshold ``t``           |
|          +--------+-----------+--------+---------+-----------+
|          | n - 1  | OnGoing   | false  | t - d   | 0         |
|          +--------+-----------+--------+---------+-----------+
|          | n      | Triggered | true   | t       | 0.01      |
|          +--------+-----------+--------+---------+-----------+
|          | n + 1  | Triggered | true   | t + d   | 0.02      |
|          +--------+-----------+--------+---------+-----------+
|          |              Repeating until release              |
|          +--------+-----------+--------+---------+-----------+
|          | m      | Triggered | true   | 0.03    | 0.03      |
|          +--------+-----------+--------+---------+-----------+
|          | m + 1  | Completed | false  | 0.03    | 0.03      |
+----------+--------+-----------+--------+---------+-----------+


* UInputTriggerTap

Triggers only if the input gets released before the deadline.
If the the input gets released late ``OnGoing`` will the last event the engine will send

+----------+--------+-----------+--------+---------+-----------+
| Trigger  | Events | Name      | Action | Elapsed | Triggered |
+----------+--------+-----------+--------+---------+-----------+
| Tap      |  1     | Started   | false  | 0.01    | 0         |
|          +--------+-----------+--------+---------+-----------+
|          |  2     | OnGoing   | false  | 0.02    | 0         |
|          +--------+-----------+--------+---------+-----------+
|          |          Repeating until release                  |
|          +--------+-----------+--------+---------+-----------+
|          | n - 1  | OnGoing   | false  | 0.03    | 0         |
|          +--------+-----------+--------+---------+-----------+
|          | n      | Triggered | false  | 0.04    | 0.01      |
|          +--------+-----------+--------+---------+-----------+
|          | n + 1  | Completed | false  | 0.04    | 0.01      |
+----------+--------+-----------+--------+---------+-----------+


* UInputTriggerHoldAndRelease

Same as release but needs to be held for a minimum amout of time
before being released

+----------+--------+-----------+--------+---------+-----------+
| Trigger  | Events | Name      | Action | Elapsed | Triggered |
+----------+--------+-----------+--------+---------+-----------+
| Hold     |  1     | Started   | false  | 0.01    | 0         |
|          +--------+-----------+--------+---------+-----------+
|          |  2     | OnGoing   | false  | 0.02    | 0         |
|          +--------+-----------+--------+---------+-----------+
|          |          Repeating until release                  |
|          +--------+-----------+--------+---------+-----------+
|          | n - 1  | OnGoing   | false  | t - d   | 0         |
|          +--------+-----------+--------+---------+-----------+
|          | n      | Triggered | false  | t       | 0.01      |
|          +--------+-----------+--------+---------+-----------+
|          | n + 1  | Completed | false  | t       | 0.01      |
+----------+--------+-----------+--------+---------+-----------+

* UInputTriggerPulse

Triggered periodically as long as the input is pressed.

+----------+--------+-----------+--------+---------+-----------+
| Trigger  | Events | Name      | Action | Elapsed | Triggered |
+----------+--------+-----------+--------+---------+-----------+
| Pulse    | 1      | Triggered | true   | 0.01    | 0.01      |
|          +--------+-----------+--------+---------+-----------+
|          | 2      | Started   | true   | 0.01    | 0.01      |
|          +--------+-----------+--------+---------+-----------+
|          | 3      | OnGoing   | false  | 0.02    | 0         |
|          +--------+-----------+--------+---------+-----------+
|          | n - 1  | OnGoing   | false  | 1 - d   | 0         |
|          +--------+-----------+--------+---------+-----------+
|          | n      | Triggered | true   | 1       | 0.01      |
|          +--------+-----------+--------+---------+-----------+
|          | n + 1  | OnGoing   | false  | 1 + d   | 0.01      |
|          +--------+-----------+--------+---------+-----------+
|          | n + 2  | OnGoing   | false  | 1 + 2d  | 0         |
+----------+--------+-----------+--------+---------+-----------+


Limitations
-----------

* If you require an input event to tick for every frame or periodically this will not work
  An event must occur or an input needs to be actuated to the entire Input system to be triggered.
  Which means if an input is only Mouse-XY then it will only get triggered when something else
  gets triggered.
  Mouse movement alone does not trigger the input system.


.. note::

   Gameplay Ablities have their own input mechanism which is not compatible with Enhanced Input
   You can use EnhancedInput and GameplayAbilities since GameplayAbilities is not using the input component.


References
----------

.. [1]: `UE4 EnhancedInput <https://docs.unrealengine.com/4.27/en-US/InteractiveExperiences/Input/EnhancedInput/>`_
.. [2]: `API Documentation <https://docs.unrealengine.com/4.26/en-US/API/Plugins/EnhancedInput/>`_
.. [3]: `Gameplay Ability Input <https://github.com/tranek/GASDocumentation#concepts-ga-input>`_
