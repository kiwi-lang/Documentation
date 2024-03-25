


FMessageLog("Blueprint").Warning(LOCTEXT("RenderTargetSampleUV_InvalidRenderTarget", "RenderTargetSampleUVEditoOnly: Render Target must be non-null."));




DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_OneParam(
    FActorBeginCursorOverSignature,     // SparseDelegateClass
    AActor,                             // OwningClass
    OnBeginCursorOver,                  // DelegateName
    AActor*,                            // Param1Type
    TouchedActor                        // Param1Name
);

UPROPERTY(BlueprintAssignable, Category = "Collision")
FWhateverDelegate OnWhatever;




Hot Fix
-------


*  Unreal Engine cannot find git
   Reason: UE expects a system wide git installation
   Solution (1): Install git on your system
   Solution (2): Link your local install to the expected location

.. code-block::

    - [  0][E][LogWindows              ]  CreateProc failed: The system cannot find the file specified. (0x00000002)
    - [  0][E][LogWindows              ]  URL: C:/Program Files/Git/bin/git.exe version
    - [  0][E][LogWindows              ]  CreateProc failed: The system cannot find the file specified. (0x00000002)
    - [  0][E][LogWindows              ]  URL: C:/Program Files (x86)/Git/bin/git.exe version

    mklink /J bin C:\Users\Newton\AppData\Local\Programs\Git\bin








	/** Data for the UI representation of this effect. This should include things like text, icons, etc. Not available in server-only builds. */
	UPROPERTY(EditDefaultsOnly, Instanced, BlueprintReadOnly, Category = Display)
	class UGameplayEffectUIData* UIData;