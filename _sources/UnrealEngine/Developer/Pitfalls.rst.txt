Pitfalls
========


RTS
---

* You need one controller per pawn (for multiplayer games)

It might be tempting to try to implement a single controller that can issue commands to multiple pawns.
but, the ``UCharacterMovementComponent`` expects the PlayerController and its AcknowledgedPawn to match
the pawn being moved (which essentially would force you to possess/unpossess every pawn.


.. code-block::

   void UCharacterMovementComponent::ReplicateMoveToServer(float DeltaTime, const FVector& NewAcceleration)
   {
      SCOPE_CYCLE_COUNTER(STAT_CharacterMovementReplicateMoveToServer);
      check(CharacterOwner != NULL);

      // Can only start sending moves if our controllers are synced up over the network, otherwise we flood the reliable buffer.
      APlayerController* PC = Cast<APlayerController>(CharacterOwner->GetController());
      if (PC && PC->AcknowledgedPawn != CharacterOwner)
      {
         return;
      }

#. Spawn a AI Controller for each pawn. The pawn becomes controlled by the authority
   Player issue commands to the AI Controllers it owns.
   The problem with this approach is you have to give up on client prediction


#. Extend the ``UCharacterMovementComponent`` and modify the Acknowledged Pawn check.
   You will need to implement a customized ACharacter that use the extend CharacterMovement component you created

.. code-block::

   AGKRTSController* PC = Cast<AGKRTSController>(CharacterOwner->GetController());

      if (PC && PC->IsPossessing(CharacterOwner))
      {
         return;
      }

.. code-block::

   AGKCharacterBase::AGKCharacterBase(const FObjectInitializer& ObjectInitializer):
    Super(ObjectInitializer.SetDefaultSubobjectClass<UGKRTSCharMovementComponent>(ACharacter::CharacterMovementComponentName))
   {

   }
