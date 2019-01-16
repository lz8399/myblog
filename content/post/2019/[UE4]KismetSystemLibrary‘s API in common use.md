+++
title= "[UE4]KismetSystemLibrary‘s API in common use"
date= "2019-01-16T15:42:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "KismetSystemLibrary", "UKismetSystemLibrary"]
thumbnailImage= "/thumbnail/cover-japan-001.jpg"
autoThumbnailImage= "true"
thumbnailImagePosition= "top"
+++

keywords: KismetSystemLibrary, UKismetSystemLibrary

<!--more-->

##### Direction and OS

	/** Get the directory of the current project */
	UFUNCTION(BlueprintPure, Category="Utilities|Paths", meta=(BlueprintThreadSafe))
	static FString GetProjectDirectory();

	/** Get the content directory of the current project */
	UFUNCTION(BlueprintPure, Category="Utilities|Paths", meta=(BlueprintThreadSafe))
	static FString GetProjectContentDirectory();

	/** Get the saved directory of the current project */
	UFUNCTION(BlueprintPure, Category="Utilities|Paths", meta=(BlueprintThreadSafe))
	static FString GetProjectSavedDirectory();
	
	/** Get the current user name from the OS */
	UFUNCTION(BlueprintPure, Category="Utilities|Platform")
	static FString GetPlatformUserName();
	
	/** 
	 * Get the current game time, in seconds. This stops when the game is paused and is affected by slomo. 
	 * 
	 * @param WorldContextObject	World context
	 */
	UFUNCTION(BlueprintPure, Category="Utilities|Time", meta=(WorldContext="WorldContextObject") )
	static float GetGameTimeInSeconds(UObject* WorldContextObject);
	
##### Object 

	UFUNCTION(BlueprintPure, Category="Utilities")
	static bool DoesImplementInterface(UObject* TestObject, TSubclassOf<UInterface> Interface);
	
##### Server & Building
	
	/** Returns whether the world this object is in is the host or not */
	UFUNCTION(BlueprintPure, Category="Networking", meta=(WorldContext="WorldContextObject") )
	static bool IsServer(UObject* WorldContextObject);

	/** Returns whether this is running on a dedicated server */
	UFUNCTION(BlueprintPure, Category="Networking", meta=(WorldContext="WorldContextObject"))
	static bool IsDedicatedServer(UObject* WorldContextObject);

	/** Returns whether this game instance is stand alone (no networking). */
	UFUNCTION(BlueprintPure, Category="Networking", meta=(WorldContext="WorldContextObject"))
	static bool IsStandalone(UObject* WorldContextObject);
	
	/** Returns whether this is a build that is packaged for distribution */
	UFUNCTION(BlueprintPure, Category="Development", meta=(BlueprintThreadSafe))
	static bool IsPackagedForDistribution();
	
##### Device

	/** Returns the platform specific unique device id */
	UFUNCTION(BlueprintPure, Category="Utilities|Platform", meta = (DeprecatedFunction, DeprecationMessage = "Use GetDeviceId instead"))
	static FString GetUniqueDeviceId();
	
##### Log
	
	/**
	 * Prints a string to the log, and optionally, to the screen
	 * If Print To Log is true, it will be visible in the Output Log window.  Otherwise it will be logged only as 'Verbose', so it generally won't show up.
	 *
	 * @param	InString		The string to log out
	 * @param	bPrintToScreen	Whether or not to print the output to the screen
	 * @param	bPrintToLog		Whether or not to print the output to the log
	 * @param	bPrintToConsole	Whether or not to print the output to the console
	 * @param	TextColor		Whether or not to print the output to the console
	 * @param	Duration		The display duration (if Print to Screen is True). Using negative number will result in loading the duration time from the config.
	 */
	UFUNCTION(BlueprintCallable, meta=(WorldContext="WorldContextObject", CallableWithoutWorldContext, Keywords = "log print", AdvancedDisplay = "2", DevelopmentOnly), Category="Utilities|String")
	static void PrintString(UObject* WorldContextObject, const FString& InString = FString(TEXT("Hello")), bool bPrintToScreen = true, bool bPrintToLog = true, FLinearColor TextColor = FLinearColor(0.0, 0.66, 1.0), float Duration = 2.f);

	/**
	 * Prints text to the log, and optionally, to the screen
	 * If Print To Log is true, it will be visible in the Output Log window.  Otherwise it will be logged only as 'Verbose', so it generally won't show up.
	 *
	 * @param	InText			The text to log out
	 * @param	bPrintToScreen	Whether or not to print the output to the screen
	 * @param	bPrintToLog		Whether or not to print the output to the log
	 * @param	bPrintToConsole	Whether or not to print the output to the console
	 * @param	TextColor		Whether or not to print the output to the console
	 * @param	Duration		The display duration (if Print to Screen is True). Using negative number will result in loading the duration time from the config.
	 */
	UFUNCTION(BlueprintCallable, meta=(WorldContext="WorldContextObject", CallableWithoutWorldContext, Keywords = "log", AdvancedDisplay = "2", DevelopmentOnly), Category="Utilities|Text")
	static void PrintText(UObject* WorldContextObject, const FText InText = INVTEXT("Hello"), bool bPrintToScreen = true, bool bPrintToLog = true, FLinearColor TextColor = FLinearColor(0.0, 0.66, 1.0), float Duration = 2.f);

	/**
	 * Prints a warning string to the log and the screen. Meant to be used as a way to inform the user that they misused the node.
	 *
	 * WARNING!! Don't change the signature of this function without fixing up all nodes using it in the compiler
	 *
	 * @param	InString		The string to log out
	 */
	UFUNCTION(BlueprintCallable, meta=(BlueprintInternalUseOnly = "TRUE"))
	static void PrintWarning(const FString& InString);

	/** Sets the game window title */
	UFUNCTION(BlueprintCallable, Category = "Utilities")
	static void SetWindowTitle(const FText& Title);
	
##### Console

	/**
	 * Executes a console command, optionally on a specific controller
	 * 
	 * @param	Command			Command to send to the console
	 * @param	SpecificPlayer	If specified, the console command will be routed through the specified player
	 */
	UFUNCTION(BlueprintCallable, Category="Development",meta=(WorldContext="WorldContextObject"))
	static void ExecuteConsoleCommand(UObject* WorldContextObject, const FString& Command, class APlayerController* SpecificPlayer = NULL );

	/**
	 * Attempts to retrieve the value of the specified float console variable, if it exists.
	 * 
	 * @param	VariableName	Name of the console variable to find.
	 * @return	The value if found, 0 otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Development",meta=(WorldContext="WorldContextObject"))
	static float GetConsoleVariableFloatValue(UObject* WorldContextObject, const FString& VariableName);

	/**
	 * Attempts to retrieve the value of the specified integer console variable, if it exists.
	 * 
	 * @param	VariableName	Name of the console variable to find.
	 * @return	The value if found, 0 otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Development",meta=(WorldContext="WorldContextObject"))
	static int32 GetConsoleVariableIntValue(UObject* WorldContextObject, const FString& VariableName);

	/** 
	 *	Exit the current game 
	 * @param	SpecificPlayer	The specific player to quit the game. If not specified, player 0 will quit.
	 * @param	QuitPreference	Form of quitting.
	 * @param	bIgnorePlatformRestrictions	Ignores and best-practices based on platform (e.g PS4 games should never quit). Non-shipping only
	 */
	UFUNCTION(BlueprintCallable, Category="Game",meta=(WorldContext="WorldContextObject"))
	static void QuitGame(UObject* WorldContextObject, class APlayerController* SpecificPlayer, TEnumAsByte<EQuitPreference::Type> QuitPreference, bool bIgnorePlatformRestrictions);
	
	
##### Latent Actions

	/** 
	 * Perform a latent action with a delay (specified in seconds).  Calling again while it is counting down will be ignored.
	 * 
	 * @param WorldContext	World context.
	 * @param Duration 		length of delay (in seconds).
	 * @param LatentInfo 	The latent action.
	 */
	UFUNCTION(BlueprintCallable, Category="Utilities|FlowControl", meta=(Latent, WorldContext="WorldContextObject", LatentInfo="LatentInfo", Duration="0.2", Keywords="sleep"))
	static void	Delay(UObject* WorldContextObject, float Duration, struct FLatentActionInfo LatentInfo );

	/** 
	 * Perform a latent action with a retriggerable delay (specified in seconds).  Calling again while it is counting down will reset the countdown to Duration.
	 * 
	 * @param WorldContext	World context.
	 * @param Duration 		length of delay (in seconds).
	 * @param LatentInfo 	The latent action.
	 */
	UFUNCTION(BlueprintCallable, meta=(Latent, LatentInfo="LatentInfo", WorldContext="WorldContextObject", Duration="0.2", Keywords="sleep"), Category="Utilities|FlowControl")
	static void RetriggerableDelay(UObject* WorldContextObject, float Duration, FLatentActionInfo LatentInfo);

	/*
	 * Interpolate a component to the specified relative location and rotation over the course of OverTime seconds. 
	 * @param Component						Component to interpolate
	 * @param TargetRelativeLocation		Relative target location
	 * @param TargetRelativeRotation		Relative target rotation
	 * @param bEaseOut						if true we will ease out (ie end slowly) during interpolation
	 * @param bEaseIn						if true we will ease in (ie start slowly) during interpolation
	 * @param OverTime						duration of interpolation
	 * @param bForceShortestRotationPath	if true we will always use the shortest path for rotation
	 * @param MoveAction					required movement behavior @see EMoveComponentAction
	 * @param LatentInfo					The latent action
	 */
	UFUNCTION(BlueprintCallable, meta=(Latent, LatentInfo="LatentInfo", WorldContext="WorldContextObject", ExpandEnumAsExecs="MoveAction", OverTime="0.2"), Category="Components")
	static void MoveComponentTo(USceneComponent* Component, FVector TargetRelativeLocation, FRotator TargetRelativeRotation, bool bEaseOut, bool bEaseIn, float OverTime, bool bForceShortestRotationPath, TEnumAsByte<EMoveComponentAction::Type> MoveAction, FLatentActionInfo LatentInfo);
	
##### 'Set property by name' functions

	// --- 'Set property by name' functions ------------------------------

	/** Set an int32 property by name */
	UFUNCTION(BlueprintCallable, meta=(BlueprintInternalUseOnly = "true"))
	static void SetIntPropertyByName(UObject* Object, FName PropertyName, int32 Value);

	/** Set an uint8 or enum property by name */
	UFUNCTION(BlueprintCallable, meta=(BlueprintInternalUseOnly = "true"))
	static void SetBytePropertyByName(UObject* Object, FName PropertyName, uint8 Value);

	/** Set a float property by name */
	UFUNCTION(BlueprintCallable, meta=(BlueprintInternalUseOnly = "true"))
	static void SetFloatPropertyByName(UObject* Object, FName PropertyName, float Value);

	/** Set a bool property by name */
	UFUNCTION(BlueprintCallable, meta=(BlueprintInternalUseOnly = "true"))
	static void SetBoolPropertyByName(UObject* Object, FName PropertyName, bool Value);

	/** Set an OBJECT property by name */
	UFUNCTION(BlueprintCallable, meta=(BlueprintInternalUseOnly = "true"))
	static void SetObjectPropertyByName(UObject* Object, FName PropertyName, UObject* Value);

	/** Set a CLASS property by name */
	UFUNCTION(BlueprintCallable, meta = (BlueprintInternalUseOnly = "true"))
	static void SetClassPropertyByName(UObject* Object, FName PropertyName, TSubclassOf<UObject> Value);
	
##### Collision functions

	/**
	 * Returns an array of actors that overlap the given sphere.
	 * @param WorldContext	World context
	 * @param SpherePos		Center of sphere.
	 * @param SphereRadius	Size of sphere.
	 * @param Filter		Option to restrict results to only static or only dynamic.  For efficiency.
	 * @param ClassFilter	If set, will only return results of this class or subclasses of it.
	 * @param ActorsToIgnore		Ignore these actors in the list
	 * @param OutActors		Returned array of actors. Unsorted.
	 * @return				true if there was an overlap that passed the filters, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName = "SphereOverlapActors"))
	static bool SphereOverlapActors(UObject* WorldContextObject, const FVector SpherePos, float SphereRadius, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, UClass* ActorClassFilter, const TArray<AActor*>& ActorsToIgnore, TArray<class AActor*>& OutActors);

	/**
	 * Returns an array of components that overlap the given sphere.
	 * @param WorldContext	World context
	 * @param SpherePos		Center of sphere.
	 * @param SphereRadius	Size of sphere.
	 * @param Filter		Option to restrict results to only static or only dynamic.  For efficiency.
	 * @param ClassFilter	If set, will only return results of this class or subclasses of it.
	 * @param ActorsToIgnore		Ignore these actors in the list
	 * @param OutActors		Returned array of actors. Unsorted.
	 * @return				true if there was an overlap that passed the filters, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName="SphereOverlapComponents"))
	static bool SphereOverlapComponents(UObject* WorldContextObject, const FVector SpherePos, float SphereRadius, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, UClass* ComponentClassFilter, const TArray<AActor*>& ActorsToIgnore, TArray<class UPrimitiveComponent*>& OutComponents);
	

	/**
	 * Returns an array of actors that overlap the given axis-aligned box.
	 * @param WorldContext	World context
	 * @param BoxPos		Center of box.
	 * @param BoxExtent		Extents of box.
	 * @param Filter		Option to restrict results to only static or only dynamic.  For efficiency.
	 * @param ClassFilter	If set, will only return results of this class or subclasses of it.
	 * @param ActorsToIgnore		Ignore these actors in the list
	 * @param OutActors		Returned array of actors. Unsorted.
	 * @return				true if there was an overlap that passed the filters, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName="BoxOverlapActors"))
	static bool BoxOverlapActors(UObject* WorldContextObject, const FVector BoxPos, FVector BoxExtent, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, UClass* ActorClassFilter, const TArray<AActor*>& ActorsToIgnore, TArray<class AActor*>& OutActors);

	/**
	 * Returns an array of components that overlap the given axis-aligned box.
	 * @param WorldContext	World context
	 * @param BoxPos		Center of box.
	 * @param BoxExtent		Extents of box.
	 * @param Filter		Option to restrict results to only static or only dynamic.  For efficiency.
	 * @param ClassFilter	If set, will only return results of this class or subclasses of it.
	 * @param ActorsToIgnore		Ignore these actors in the list
	 * @param OutActors		Returned array of actors. Unsorted.
	 * @return				true if there was an overlap that passed the filters, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName="BoxOverlapComponents"))
	static bool BoxOverlapComponents(UObject* WorldContextObject, const FVector BoxPos, FVector Extent, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, UClass* ComponentClassFilter, const TArray<AActor*>& ActorsToIgnore, TArray<class UPrimitiveComponent*>& OutComponents);


	/**
	 * Returns an array of actors that overlap the given capsule.
	 * @param WorldContext	World context
	 * @param CapsulePos	Center of the capsule.
	 * @param Radius		Radius of capsule hemispheres and radius of center cylinder portion.
	 * @param HalfHeight	Half-height of the capsule (from center of capsule to tip of hemisphere.
	 * @param Filter		Option to restrict results to only static or only dynamic.  For efficiency.
	 * @param ClassFilter	If set, will only return results of this class or subclasses of it.
	 * @param ActorsToIgnore		Ignore these actors in the list
	 * @param OutActors		Returned array of actors. Unsorted.
	 * @return				true if there was an overlap that passed the filters, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName="CapsuleOverlapActors"))
	static bool CapsuleOverlapActors(UObject* WorldContextObject, const FVector CapsulePos, float Radius, float HalfHeight, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, UClass* ActorClassFilter, const TArray<AActor*>& ActorsToIgnore, TArray<class AActor*>& OutActors);

	/**
	 * Returns an array of components that overlap the given capsule.
	 * @param WorldContext	World context
	 * @param CapsulePos	Center of the capsule.
	 * @param Radius		Radius of capsule hemispheres and radius of center cylinder portion.
	 * @param HalfHeight	Half-height of the capsule (from center of capsule to tip of hemisphere.
	 * @param Filter		Option to restrict results to only static or only dynamic.  For efficiency.
	 * @param ClassFilter	If set, will only return results of this class or subclasses of it.
	 * @param ActorsToIgnore		Ignore these actors in the list
	 * @param OutActors		Returned array of actors. Unsorted.
	 * @return				true if there was an overlap that passed the filters, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName="CapsuleOverlapComponents") )
	static bool CapsuleOverlapComponents(UObject* WorldContextObject, const FVector CapsulePos, float Radius, float HalfHeight, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, UClass* ComponentClassFilter, const TArray<AActor*>& ActorsToIgnore, TArray<class UPrimitiveComponent*>& OutComponents);


	/**
	 * Returns an array of actors that overlap the given component.
	 * @param Component				Component to test with.
	 * @param ComponentTransform	Defines where to place the component for overlap testing.
	 * @param Filter				Option to restrict results to only static or only dynamic.  For efficiency.
	 * @param ClassFilter			If set, will only return results of this class or subclasses of it.
	 * @param ActorsToIgnore		Ignore these actors in the list
	 * @param OutActors				Returned array of actors. Unsorted.
	 * @return						true if there was an overlap that passed the filters, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(AutoCreateRefTerm="ActorsToIgnore", DisplayName="ComponentOverlapActors"))
	static bool ComponentOverlapActors(UPrimitiveComponent* Component, const FTransform& ComponentTransform, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, UClass* ActorClassFilter, const TArray<AActor*>& ActorsToIgnore, TArray<class AActor*>& OutActors);

	/**
	 * Returns an array of components that overlap the given component.
	 * @param Component				Component to test with.
	 * @param ComponentTransform	Defines where to place the component for overlap testing.
	 * @param Filter				Option to restrict results to only static or only dynamic.  For efficiency.
	 * @param ClassFilter			If set, will only return results of this class or subclasses of it.
	 * @param ActorsToIgnore		Ignore these actors in the list
	 * @param OutActors				Returned array of actors. Unsorted.
	 * @return						true if there was an overlap that passed the filters, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(AutoCreateRefTerm="ActorsToIgnore", DisplayName="ComponentOverlapComponents"))
	static bool ComponentOverlapComponents(UPrimitiveComponent* Component, const FTransform& ComponentTransform, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, UClass* ComponentClassFilter, const TArray<AActor*>& ActorsToIgnore, TArray<class UPrimitiveComponent*>& OutComponents);


	/**
	 * Does a collision trace along the given line and returns the first blocking hit encountered.
	 * This trace finds the objects that RESPONDS to the given TraceChannel
	 * 
	 * @param WorldContext	World context
	 * @param Start			Start of line segment.
	 * @param End			End of line segment.
	 * @param TraceChannel	
	 * @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	 * @param OutHit		Properties of the trace hit.
	 * @return				True if there was a hit, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(bIgnoreSelf="true", WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName="LineTraceByChannel", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="raycast"))
	static bool LineTraceSingle(UObject* WorldContextObject, const FVector Start, const FVector End, ETraceTypeQuery TraceChannel, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, FHitResult& OutHit, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);
	
	/**
	 * Does a collision trace along the given line and returns all hits encountered up to and including the first blocking hit.
	 * This trace finds the objects that RESPOND to the given TraceChannel
	 * 
	 * @param WorldContext	World context
	 * @param Start			Start of line segment.
	 * @param End			End of line segment.
	 * @param TraceChannel	The channel to trace
	 * @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	 * @param OutHit		Properties of the trace hit.
	 * @return				True if there was a blocking hit, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(bIgnoreSelf="true", WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName = "MultiLineTraceByChannel", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="raycast"))
	static bool LineTraceMulti(UObject* WorldContextObject, const FVector Start, const FVector End, ETraceTypeQuery TraceChannel, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, TArray<FHitResult>& OutHits, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	 * Sweeps a sphere along the given line and returns the first blocking hit encountered.
	 * This trace finds the objects that RESPONDS to the given TraceChannel
	 * 
	 * @param Start			Start of line segment.
	 * @param End			End of line segment.
	 * @param Radius		Radius of the sphere to sweep
	 * @param TraceChannel	
	 * @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	 * @param OutHit		Properties of the trace hit.
	 * @return				True if there was a hit, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(bIgnoreSelf="true", WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName = "SphereTraceByChannel", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="sweep"))
	static bool SphereTraceSingle(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius, ETraceTypeQuery TraceChannel, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, FHitResult& OutHit, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	 * Sweeps a sphere along the given line and returns all hits encountered up to and including the first blocking hit.
	 * This trace finds the objects that RESPOND to the given TraceChannel
	 * 
	 * @param WorldContext	World context
	 * @param Start			Start of line segment.
	 * @param End			End of line segment.
	 * @param Radius		Radius of the sphere to sweep
	 * @param TraceChannel	
	 * @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	 * @param OutHits		A list of hits, sorted along the trace from start to finish.  The blocking hit will be the last hit, if there was one.
	 * @return				True if there was a blocking hit, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(bIgnoreSelf="true", WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName = "MultiSphereTraceByChannel", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="sweep"))
	static bool SphereTraceMulti(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius, ETraceTypeQuery TraceChannel, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, TArray<FHitResult>& OutHits, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	* Sweeps a box along the given line and returns the first blocking hit encountered.
	* This trace finds the objects that RESPONDS to the given TraceChannel
	*
	* @param Start			Start of line segment.
	* @param End			End of line segment.
	* @param HalfSize	    Distance from the center of box along each axis
	* @param Orientation	Orientation of the box
	* @param TraceChannel
	* @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	* @param OutHit			Properties of the trace hit.
	* @return				True if there was a hit, false otherwise.
	*/
	UFUNCTION(BlueprintCallable, Category = "Collision", meta = (bIgnoreSelf = "true", WorldContext="WorldContextObject", AutoCreateRefTerm = "ActorsToIgnore", DisplayName = "BoxTraceByChannel", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="sweep"))
	static bool BoxTraceSingle(UObject* WorldContextObject, const FVector Start, const FVector End, const FVector HalfSize, const FRotator Orientation, ETraceTypeQuery TraceChannel, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, FHitResult& OutHit, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	* Sweeps a box along the given line and returns all hits encountered.
	* This trace finds the objects that RESPONDS to the given TraceChannel
	*
	* @param Start			Start of line segment.
	* @param End			End of line segment.
	* @param HalfSize	    Distance from the center of box along each axis
	* @param Orientation	Orientation of the box
	* @param TraceChannel
	* @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	* @param OutHits		A list of hits, sorted along the trace from start to finish. The blocking hit will be the last hit, if there was one.
	* @return				True if there was a blocking hit, false otherwise.
	*/
	UFUNCTION(BlueprintCallable, Category = "Collision", meta = (bIgnoreSelf = "true", WorldContext="WorldContextObject", AutoCreateRefTerm = "ActorsToIgnore", DisplayName = "MultiBoxTraceByChannel", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="sweep"))
	static bool BoxTraceMulti(UObject* WorldContextObject, const FVector Start, const FVector End, FVector HalfSize, const FRotator Orientation, ETraceTypeQuery TraceChannel, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, TArray<FHitResult>& OutHits, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	
	/**
	 * Sweeps a capsule along the given line and returns the first blocking hit encountered.
	 * This trace finds the objects that RESPOND to the given TraceChannel
	 * 
	 * @param WorldContext	World context
	 * @param Start			Start of line segment.
	 * @param End			End of line segment.
	 * @param Radius		Radius of the capsule to sweep
	 * @param HalfHeight	Distance from center of capsule to tip of hemisphere endcap.
	 * @param TraceChannel	
	 * @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	 * @param OutHit		Properties of the trace hit.
	 * @return				True if there was a hit, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(bIgnoreSelf="true", WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName = "CapsuleTraceByChannel", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="sweep"))
	static bool CapsuleTraceSingle(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius, float HalfHeight, ETraceTypeQuery TraceChannel, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, FHitResult& OutHit, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	 * Sweeps a capsule along the given line and returns all hits encountered up to and including the first blocking hit.
	 * This trace finds the objects that RESPOND to the given TraceChannel
	 * 
	 * @param WorldContext	World context
	 * @param Start			Start of line segment.
	 * @param End			End of line segment.
	 * @param Radius		Radius of the capsule to sweep
	 * @param HalfHeight	Distance from center of capsule to tip of hemisphere endcap.
	 * @param TraceChannel	
	 * @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	 * @param OutHits		A list of hits, sorted along the trace from start to finish.  The blocking hit will be the last hit, if there was one.
	 * @return				True if there was a blocking hit, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(bIgnoreSelf="true", WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName = "MultiCapsuleTraceByChannel", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="sweep"))
	static bool CapsuleTraceMulti(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius, float HalfHeight, ETraceTypeQuery TraceChannel, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, TArray<FHitResult>& OutHits, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	 * Does a collision trace along the given line and returns the first hit encountered.
	 * This only finds objects that are of a type specified by ObjectTypes.
	 * 
	 * @param WorldContext	World context
	 * @param Start			Start of line segment.
	 * @param End			End of line segment.
	 * @param ObjectTypes	Array of Object Types to trace 
	 * @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	 * @param OutHit		Properties of the trace hit.
	 * @return				True if there was a hit, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(bIgnoreSelf="true", WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName = "LineTraceForObjects", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="raycast"))
	static bool LineTraceSingleForObjects(UObject* WorldContextObject, const FVector Start, const FVector End, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, FHitResult& OutHit, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f );
	
	/**
	 * Does a collision trace along the given line and returns all hits encountered.
	 * This only finds objects that are of a type specified by ObjectTypes.
	 * 
	 * @param WorldContext	World context
	 * @param Start			Start of line segment.
	 * @param End			End of line segment.
	 * @param ObjectTypes	Array of Object Types to trace 
	 * @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	 * @param OutHit		Properties of the trace hit.
	 * @return				True if there was a hit, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(bIgnoreSelf="true", WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName = "MultiLineTraceForObjects", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="raycast"))
	static bool LineTraceMultiForObjects(UObject* WorldContextObject, const FVector Start, const FVector End, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, TArray<FHitResult>& OutHits, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	 * Sweeps a sphere along the given line and returns the first hit encountered.
	 * This only finds objects that are of a type specified by ObjectTypes.
	 * 
	 * @param Start			Start of line segment.
	 * @param End			End of line segment.
	 * @param Radius		Radius of the sphere to sweep
	 * @param ObjectTypes	Array of Object Types to trace 
	 * @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	 * @param OutHit		Properties of the trace hit.
	 * @return				True if there was a hit, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(bIgnoreSelf="true", WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName = "SphereTraceForObjects", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="sweep"))
	static bool SphereTraceSingleForObjects(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, FHitResult& OutHit, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	 * Sweeps a sphere along the given line and returns all hits encountered.
	 * This only finds objects that are of a type specified by ObjectTypes.
	 * 
	 * @param WorldContext	World context
	 * @param Start			Start of line segment.
	 * @param End			End of line segment.
	 * @param Radius		Radius of the sphere to sweep
	 * @param ObjectTypes	Array of Object Types to trace 
	 * @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	 * @param OutHits		A list of hits, sorted along the trace from start to finish.  The blocking hit will be the last hit, if there was one.
	 * @return				True if there was a hit, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(bIgnoreSelf="true", WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName = "MultiSphereTraceForObjects", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="sweep"))
	static bool SphereTraceMultiForObjects(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, TArray<FHitResult>& OutHits, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);
	

	/**
	* Sweeps a box along the given line and returns the first hit encountered.
	* This only finds objects that are of a type specified by ObjectTypes.
	*
	* @param Start			Start of line segment.
	* @param End			End of line segment.
	* @param Orientation	
	* @param HalfSize		Radius of the sphere to sweep
	* @param ObjectTypes	Array of Object Types to trace
	* @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	* @param OutHit			Properties of the trace hit.
	* @return				True if there was a hit, false otherwise.
	*/
	UFUNCTION(BlueprintCallable, Category = "Collision", meta = (bIgnoreSelf = "true", WorldContext="WorldContextObject", AutoCreateRefTerm = "ActorsToIgnore", DisplayName = "BoxTraceForObjects", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="sweep"))
	static bool BoxTraceSingleForObjects(UObject* WorldContextObject, const FVector Start, const FVector End, const FVector HalfSize, const FRotator Orientation, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, FHitResult& OutHit, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);


	/**
	* Sweeps a box along the given line and returns all hits encountered.
	* This only finds objects that are of a type specified by ObjectTypes.
	*
	* @param Start			Start of line segment.
	* @param End			End of line segment.
	* @param Orientation
	* @param HalfSize		Radius of the sphere to sweep
	* @param ObjectTypes	Array of Object Types to trace
	* @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	* @param OutHits		A list of hits, sorted along the trace from start to finish.  The blocking hit will be the last hit, if there was one.
	* @return				True if there was a hit, false otherwise.
	*/
	UFUNCTION(BlueprintCallable, Category = "Collision", meta = (bIgnoreSelf = "true", WorldContext="WorldContextObject", AutoCreateRefTerm = "ActorsToIgnore", DisplayName = "MultiBoxTraceForObjects", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="sweep"))
	static bool BoxTraceMultiForObjects(UObject* WorldContextObject, const FVector Start, const FVector End, const FVector HalfSize, const FRotator Orientation, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, TArray<FHitResult>& OutHits, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	 * Sweeps a capsule along the given line and returns the first hit encountered.
	 * This only finds objects that are of a type specified by ObjectTypes.
	 * 
	 * @param WorldContext	World context
	 * @param Start			Start of line segment.
	 * @param End			End of line segment.
	 * @param Radius		Radius of the capsule to sweep
	 * @param HalfHeight	Distance from center of capsule to tip of hemisphere endcap.
	 * @param ObjectTypes	Array of Object Types to trace 
	 * @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	 * @param OutHit		Properties of the trace hit.
	 * @return				True if there was a hit, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(bIgnoreSelf="true", WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName = "CapsuleTraceForObjects", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="sweep"))
	static bool CapsuleTraceSingleForObjects(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius, float HalfHeight, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, FHitResult& OutHit, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	 * Sweeps a capsule along the given line and returns all hits encountered.
	 * This only finds objects that are of a type specified by ObjectTypes.
	 * 
	 * @param WorldContext	World context
	 * @param Start			Start of line segment.
	 * @param End			End of line segment.
	 * @param Radius		Radius of the capsule to sweep
	 * @param HalfHeight	Distance from center of capsule to tip of hemisphere endcap.
	 * @param ObjectTypes	Array of Object Types to trace 
	 * @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	 * @param OutHits		A list of hits, sorted along the trace from start to finish.  The blocking hit will be the last hit, if there was one.
	 * @return				True if there was a hit, false otherwise.
	 */
	UFUNCTION(BlueprintCallable, Category="Collision", meta=(bIgnoreSelf="true", WorldContext="WorldContextObject", AutoCreateRefTerm="ActorsToIgnore", DisplayName = "MultiCapsuleTraceForObjects", AdvancedDisplay="TraceColor,TraceHitColor,DrawTime", Keywords="sweep"))
	static bool CapsuleTraceMultiForObjects(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius, float HalfHeight, const TArray<TEnumAsByte<EObjectTypeQuery> > & ObjectTypes, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, TArray<FHitResult>& OutHits, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	// BY PROFILE

	/**
	* Trace a ray against the world using a specific profile and return the first blocking hit
	*
	* @param WorldContext	World context
	* @param Start			Start of line segment.
	* @param End			End of line segment.
	* @param ProfileName	The 'profile' used to determine which components to hit
	* @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	* @param OutHit			Properties of the trace hit.
	* @return				True if there was a hit, false otherwise.
	*/
	UFUNCTION(BlueprintCallable, Category = "Collision", meta = (bIgnoreSelf = "true", WorldContext = "WorldContextObject", AutoCreateRefTerm = "ActorsToIgnore", DisplayName = "LineTraceByProfile", AdvancedDisplay = "TraceColor,TraceHitColor,DrawTime", Keywords = "raycast"))
	static bool LineTraceSingleByProfile(UObject* WorldContextObject, const FVector Start, const FVector End, FName ProfileName, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, FHitResult& OutHit, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	*  Trace a ray against the world using a specific profile and return overlapping hits and then first blocking hit
	*  Results are sorted, so a blocking hit (if found) will be the last element of the array
	*  Only the single closest blocking result will be generated, no tests will be done after that
	*
	* @param WorldContext	World context
	* @param Start			Start of line segment.
	* @param End			End of line segment.
	* @param ProfileName	The 'profile' used to determine which components to hit
	* @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	* @param OutHit		Properties of the trace hit.
	* @return				True if there was a blocking hit, false otherwise.
	*/
	UFUNCTION(BlueprintCallable, Category = "Collision", meta = (bIgnoreSelf = "true", WorldContext = "WorldContextObject", AutoCreateRefTerm = "ActorsToIgnore", DisplayName = "MultiLineTraceByProfile", AdvancedDisplay = "TraceColor,TraceHitColor,DrawTime", Keywords = "raycast"))
	static bool LineTraceMultiByProfile(UObject* WorldContextObject, const FVector Start, const FVector End, FName ProfileName, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, TArray<FHitResult>& OutHits, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	*  Sweep a sphere against the world and return the first blocking hit using a specific profile
	*
	* @param Start			Start of line segment.
	* @param End			End of line segment.
	* @param Radius			Radius of the sphere to sweep
	* @param ProfileName	The 'profile' used to determine which components to hit
	* @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	* @param OutHit			Properties of the trace hit.
	* @return				True if there was a hit, false otherwise.
	*/
	UFUNCTION(BlueprintCallable, Category = "Collision", meta = (bIgnoreSelf = "true", WorldContext = "WorldContextObject", AutoCreateRefTerm = "ActorsToIgnore", DisplayName = "SphereTraceByProfile", AdvancedDisplay = "TraceColor,TraceHitColor,DrawTime", Keywords = "sweep"))
	static bool SphereTraceSingleByProfile(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius, FName ProfileName, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, FHitResult& OutHit, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	*  Sweep a sphere against the world and return all initial overlaps using a specific profile, then overlapping hits and then first blocking hit
	*  Results are sorted, so a blocking hit (if found) will be the last element of the array
	*  Only the single closest blocking result will be generated, no tests will be done after that
	*
	* @param WorldContext	World context
	* @param Start			Start of line segment.
	* @param End			End of line segment.
	* @param Radius		Radius of the sphere to sweep
	* @param ProfileName	The 'profile' used to determine which components to hit
	* @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	* @param OutHits		A list of hits, sorted along the trace from start to finish.  The blocking hit will be the last hit, if there was one.
	* @return				True if there was a blocking hit, false otherwise.
	*/
	UFUNCTION(BlueprintCallable, Category = "Collision", meta = (bIgnoreSelf = "true", WorldContext = "WorldContextObject", AutoCreateRefTerm = "ActorsToIgnore", DisplayName = "MultiSphereTraceByProfile", AdvancedDisplay = "TraceColor,TraceHitColor,DrawTime", Keywords = "sweep"))
	static bool SphereTraceMultiByProfile(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius, FName ProfileName, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, TArray<FHitResult>& OutHits, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	*  Sweep a box against the world and return the first blocking hit using a specific profile
	*
	* @param Start			Start of line segment.
	* @param End			End of line segment.
	* @param HalfSize	    Distance from the center of box along each axis
	* @param Orientation	Orientation of the box
	* @param ProfileName	The 'profile' used to determine which components to hit
	* @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	* @param OutHit			Properties of the trace hit.
	* @return				True if there was a hit, false otherwise.
	*/
	UFUNCTION(BlueprintCallable, Category = "Collision", meta = (bIgnoreSelf = "true", WorldContext = "WorldContextObject", AutoCreateRefTerm = "ActorsToIgnore", DisplayName = "BoxTraceByProfile", AdvancedDisplay = "TraceColor,TraceHitColor,DrawTime", Keywords = "sweep"))
	static bool BoxTraceSingleByProfile(UObject* WorldContextObject, const FVector Start, const FVector End, const FVector HalfSize, const FRotator Orientation, FName ProfileName, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, FHitResult& OutHit, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	*  Sweep a box against the world and return all initial overlaps using a specific profile, then overlapping hits and then first blocking hit
	*  Results are sorted, so a blocking hit (if found) will be the last element of the array
	*  Only the single closest blocking result will be generated, no tests will be done after that
	*
	* @param Start			Start of line segment.
	* @param End			End of line segment.
	* @param HalfSize	    Distance from the center of box along each axis
	* @param Orientation	Orientation of the box
	* @param ProfileName	The 'profile' used to determine which components to hit
	* @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	* @param OutHits		A list of hits, sorted along the trace from start to finish. The blocking hit will be the last hit, if there was one.
	* @return				True if there was a blocking hit, false otherwise.
	*/
	UFUNCTION(BlueprintCallable, Category = "Collision", meta = (bIgnoreSelf = "true", WorldContext = "WorldContextObject", AutoCreateRefTerm = "ActorsToIgnore", DisplayName = "MultiBoxTraceByProfile", AdvancedDisplay = "TraceColor,TraceHitColor,DrawTime", Keywords = "sweep"))
	static bool BoxTraceMultiByProfile(UObject* WorldContextObject, const FVector Start, const FVector End, FVector HalfSize, const FRotator Orientation, FName ProfileName, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, TArray<FHitResult>& OutHits, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);


	/**
	*  Sweep a capsule against the world and return the first blocking hit using a specific profile
	*
	* @param WorldContext	World context
	* @param Start			Start of line segment.
	* @param End			End of line segment.
	* @param Radius			Radius of the capsule to sweep
	* @param HalfHeight		Distance from center of capsule to tip of hemisphere endcap.
	* @param ProfileName	The 'profile' used to determine which components to hit
	* @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	* @param OutHit			Properties of the trace hit.
	* @return				True if there was a hit, false otherwise.
	*/
	UFUNCTION(BlueprintCallable, Category = "Collision", meta = (bIgnoreSelf = "true", WorldContext = "WorldContextObject", AutoCreateRefTerm = "ActorsToIgnore", DisplayName = "CapsuleTraceByProfile", AdvancedDisplay = "TraceColor,TraceHitColor,DrawTime", Keywords = "sweep"))
	static bool CapsuleTraceSingleByProfile(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius, float HalfHeight, FName ProfileName, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, FHitResult& OutHit, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);

	/**
	*  Sweep a capsule against the world and return all initial overlaps using a specific profile, then overlapping hits and then first blocking hit
	*  Results are sorted, so a blocking hit (if found) will be the last element of the array
	*  Only the single closest blocking result will be generated, no tests will be done after that
	*
	* @param WorldContext	World context
	* @param Start			Start of line segment.
	* @param End			End of line segment.
	* @param Radius			Radius of the capsule to sweep
	* @param HalfHeight		Distance from center of capsule to tip of hemisphere endcap.
	* @param ProfileName	The 'profile' used to determine which components to hit
	* @param bTraceComplex	True to test against complex collision, false to test against simplified collision.
	* @param OutHits		A list of hits, sorted along the trace from start to finish.  The blocking hit will be the last hit, if there was one.
	* @return				True if there was a blocking hit, false otherwise.
	*/
	UFUNCTION(BlueprintCallable, Category = "Collision", meta = (bIgnoreSelf = "true", WorldContext = "WorldContextObject", AutoCreateRefTerm = "ActorsToIgnore", DisplayName = "MultiCapsuleTraceByProfile", AdvancedDisplay = "TraceColor,TraceHitColor,DrawTime", Keywords = "sweep"))
	static bool CapsuleTraceMultiByProfile(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius, float HalfHeight, FName ProfileName, bool bTraceComplex, const TArray<AActor*>& ActorsToIgnore, EDrawDebugTrace::Type DrawDebugType, TArray<FHitResult>& OutHits, bool bIgnoreSelf, FLinearColor TraceColor = FLinearColor::Red, FLinearColor TraceHitColor = FLinearColor::Green, float DrawTime = 5.0f);



	/**
	 * Returns an array of unique actors represented by the given list of components.
	 * @param ComponentList		List of components.
	 * @param ClassFilter		If set, will only return results of this class or subclasses of it.
	 * @param OutActorList		Start of line segment.
	 */
	UFUNCTION(BlueprintCallable, Category="Utilities")
	static void GetActorListFromComponentList(const TArray<class UPrimitiveComponent*>& ComponentList, UClass* ActorClassFilter, TArray<class AActor*>& OutActorList);

##### Debug drawing functions

	/** Draw a debug line */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugLine(UObject* WorldContextObject, const FVector LineStart, const FVector LineEnd, FLinearColor LineColor, float Duration=0.f, float Thickness = 0.f);

	/** Draw a debug circle! */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugCircle(UObject* WorldContextObject, FVector Center, float Radius, int32 NumSegments=12, FLinearColor LineColor = FLinearColor::White, float Duration=0.f, float Thickness=0.f, FVector YAxis=FVector(0.f,1.f,0.f),FVector ZAxis=FVector(0.f,0.f,1.f), bool bDrawAxis=false);
	
	/** Draw a debug point */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugPoint(UObject* WorldContextObject, const FVector Position, float Size, FLinearColor PointColor, float Duration=0.f);

	/** Draw directional arrow, pointing from LineStart to LineEnd. */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugArrow(UObject* WorldContextObject, const FVector LineStart, const FVector LineEnd, float ArrowSize, FLinearColor LineColor, float Duration=0.f, float Thickness = 0.f);

	/** Draw a debug box */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugBox(UObject* WorldContextObject, const FVector Center, FVector Extent, FLinearColor LineColor, const FRotator Rotation=FRotator::ZeroRotator, float Duration=0.f, float Thickness = 0.f);

	/** Draw a debug coordinate system. */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugCoordinateSystem(UObject* WorldContextObject, const FVector AxisLoc, const FRotator AxisRot, float Scale=1.f, float Duration=0.f, float Thickness = 0.f);

	/** Draw a debug sphere */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugSphere(UObject* WorldContextObject, const FVector Center, float Radius=100.f, int32 Segments=12, FLinearColor LineColor = FLinearColor::White, float Duration=0.f, float Thickness = 0.f);

	/** Draw a debug cylinder */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugCylinder(UObject* WorldContextObject, const FVector Start, const FVector End, float Radius=100.f, int32 Segments=12, FLinearColor LineColor = FLinearColor::White, float Duration=0.f, float Thickness = 0.f);
	
	/** Draw a debug cone */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DeprecatedFunction, DeprecationMessage="DrawDebugCone has been changed to use degrees for angles instead of radians. Place a new DrawDebugCone node and pass your angles as degrees.", DevelopmentOnly))
	static void DrawDebugCone(UObject* WorldContextObject, const FVector Origin, const FVector Direction, float Length, float AngleWidth, float AngleHeight, int32 NumSides, FLinearColor LineColor, float Duration = 0.f, float Thickness = 0.f);

	/** 
	 * Draw a debug cone 
	 * Angles are specified in degrees
	 */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DisplayName="DrawDebugCone", DevelopmentOnly))
	static void DrawDebugConeInDegrees(UObject* WorldContextObject, const FVector Origin, const FVector Direction, float Length=100.f, float AngleWidth=45.f, float AngleHeight=45.f, int32 NumSides = 12, FLinearColor LineColor = FLinearColor::White, float Duration=0.f, float Thickness = 0.f);

	/** Draw a debug capsule */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugCapsule(UObject* WorldContextObject, const FVector Center, float HalfHeight, float Radius, const FRotator Rotation, FLinearColor LineColor = FLinearColor::White, float Duration=0.f, float Thickness = 0.f);

	/** Draw a debug string at a 3d world location. */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugString(UObject* WorldContextObject, const FVector TextLocation, const FString& Text, class AActor* TestBaseActor = NULL, FLinearColor TextColor = FLinearColor::White, float Duration=0.f);
	/** 
	 * Removes all debug strings. 
	 *
	 * @param WorldContext	World context
	 */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void FlushDebugStrings(UObject* WorldContextObject);

	/** Draws a debug plane. */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugPlane(UObject* WorldContextObject, const FPlane& PlaneCoordinates, const FVector Location, float Size, FLinearColor PlaneColor = FLinearColor::White, float Duration=0.f);

	/** 
	 * Flush all persistent debug lines and shapes.
	 *
	 * @param WorldContext	World context
	 */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void FlushPersistentDebugLines(UObject* WorldContextObject);

	/** Draws a debug frustum. */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugFrustum(UObject* WorldContextObject, const FTransform& FrustumTransform, FLinearColor FrustumColor = FLinearColor::White, float Duration=0.f, float Thickness = 0.f);

	/** Draw a debug camera shape. */
	UFUNCTION(BlueprintCallable, Category="Rendering|Debug", meta=(DevelopmentOnly))
	static void DrawDebugCamera(const ACameraActor* CameraActor, FLinearColor CameraColor = FLinearColor::White, float Duration=0.f);

	/* Draws a 2D Histogram of size 'DrawSize' based FDebugFloatHistory struct, using DrawTransform for the position in the world. */
	UFUNCTION(BlueprintCallable, Category = "Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugFloatHistoryTransform(UObject* WorldContextObject, const FDebugFloatHistory& FloatHistory, const FTransform& DrawTransform, FVector2D DrawSize, FLinearColor DrawColor = FLinearColor::White, float Duration = 0.f);

	/* Draws a 2D Histogram of size 'DrawSize' based FDebugFloatHistory struct, using DrawLocation for the location in the world, rotation will face camera of first player. */
	UFUNCTION(BlueprintCallable, Category = "Rendering|Debug", meta=(WorldContext="WorldContextObject", DevelopmentOnly))
	static void DrawDebugFloatHistoryLocation(UObject* WorldContextObject, const FDebugFloatHistory& FloatHistory, FVector DrawLocation, FVector2D DrawSize, FLinearColor DrawColor = FLinearColor::White, float Duration = 0.f);

	UFUNCTION(BlueprintCallable, Category = "Rendering|Debug", meta=(DevelopmentOnly))
	static FDebugFloatHistory AddFloatHistorySample(float Value, const FDebugFloatHistory& FloatHistory);
	
	/** Mark as modified. */
	UFUNCTION(BlueprintCallable, Category="Development|Editor")
	static void CreateCopyForUndoBuffer(UObject* ObjectToModify);

	/** Get bounds */
	UFUNCTION(BlueprintPure, Category="Collision")
	static void GetComponentBounds(const USceneComponent* Component, FVector& Origin, FVector& BoxExtent, float& SphereRadius);

	UFUNCTION(BlueprintPure, Category="Collision", meta=(DeprecatedFunction))
	static void GetActorBounds(const AActor* Actor, FVector& Origin, FVector& BoxExtent);
	
##### Get Rendering Info

	/**
	 * Get the clamped state of r.DetailMode, see console variable help (allows for scalability, cannot be used in construction scripts)
	 * 0: low, show only object with DetailMode low or higher
	 * 1: medium, show all object with DetailMode medium or higher
	 * 2: high, show all objects
	 */
	UFUNCTION(BlueprintPure, Category="Rendering", meta=(UnsafeDuringActorConstruction = "true"))
	static int32 GetRenderingDetailMode();

	/**
	 * Get the clamped state of r.MaterialQualityLevel, see console variable help (allows for scalability, cannot be used in construction scripts)
	 * 0: low
	 * 1: high
	 * 2: medium
	 */
	UFUNCTION(BlueprintPure, Category="Rendering|Material", meta=(UnsafeDuringActorConstruction = "true"))
	static int32 GetRenderingMaterialQualityLevel();

	/**
	 * Gets the list of support fullscreen resolutions.
	 * @return true if successfully queried the device for available resolutions.
	 */
	UFUNCTION(BlueprintCallable, Category="Rendering")
	static bool GetSupportedFullscreenResolutions(TArray<FIntPoint>& Resolutions);

	/**
	* Gets the list of windowed resolutions which are convenient for the current primary display size.
	* @return true if successfully queried the device for available resolutions.
	*/
	UFUNCTION(BlueprintCallable, Category="Rendering")
	static bool GetConvenientWindowedResolutions(TArray<FIntPoint>& Resolutions);

	/**
	 * Gets the smallest Y resolution we want to support in the UI, clamped within reasons
	 * @return value in pixels
	 */
	UFUNCTION(BlueprintPure, Category="Rendering", meta=(UnsafeDuringActorConstruction = "true"))
	static int32 GetMinYResolutionForUI();

	/**
	* Gets the smallest Y resolution we want to support in the 3D view, clamped within reasons
	* @return value in pixels
	*/
	UFUNCTION(BlueprintPure, Category = "Rendering", meta = (UnsafeDuringActorConstruction = "true"))
	static int32 GetMinYResolutionFor3DView();
	
##### AD banner (iAd on iOS, or AdMob on Android)

	/**
	 * Will show an ad banner (iAd on iOS, or AdMob on Android) on the top or bottom of screen, on top of the GL view (doesn't resize the view)
	 * (iOS and Android only)
	 *
	 * @param AdIdIndex The index of the ID to select for the ad to show
	 * @param bShowOnBottomOfScreen If true, the iAd will be shown at the bottom of the screen, top otherwise
	 */
	UFUNCTION(BlueprintCallable, Category = "Utilities|Platform")
	static void ShowAdBanner(int32 AdIdIndex, bool bShowOnBottomOfScreen);

	/**
	* Retrieves the total number of Ad IDs that can be selected between
	*/
	UFUNCTION(BlueprintPure, Category = "Utilities|Platform", meta = (DisplayName = "Get Ad ID Count"))
	static int32 GetAdIDCount();

	/**
	 * Hides the ad banner (iAd on iOS, or AdMob on Android). Will force close the ad if it's open
	 * (iOS and Android only)
	 */
	UFUNCTION(BlueprintCallable, Category = "Utilities|Platform")
	static void HideAdBanner();

	/**
	 * Forces closed any displayed ad. Can lead to loss of revenue
	 * (iOS and Android only)
	 */
	UFUNCTION(BlueprintCallable, Category = "Utilities|Platform")
	static void ForceCloseAdBanner();

	/**
	* Will load a fullscreen interstitial AdMob ad. Call this before using ShowInterstitialAd
	* (Android only)
	*
	* @param AdIdIndex The index of the ID to select for the ad to show
	*/
	UFUNCTION(BlueprintCallable, Category = "Utilities|Platform")
		static void LoadInterstitialAd(int32 AdIdIndex);

	/**
	* Returns true if the requested interstitial ad is loaded and ready
	* (Android only)
	*/
	UFUNCTION(BlueprintCallable, Category = "Utilities|Platform")
		static bool IsInterstitialAdAvailable();

	/**
	* Returns true if the requested interstitial ad has been successfully requested (false if load request fails)
	* (Android only)
	*/
	UFUNCTION(BlueprintCallable, Category = "Utilities|Platform")
		static bool IsInterstitialAdRequested();

	/**
	* Shows the loaded interstitial ad (loaded with LoadInterstitialAd)
	* (Android only)
	*/
	UFUNCTION(BlueprintCallable, Category = "Utilities|Platform")
		static void ShowInterstitialAd();

	/**
	 * Displays the built-in leaderboard GUI (iOS and Android only; this function may be renamed or moved in a future release)
	 */
	UFUNCTION(BlueprintCallable, Category = "Utilities|Platform")
	static void ShowPlatformSpecificLeaderboardScreen(const FString& CategoryName);

	/**
	 * Displays the built-in achievements GUI (iOS and Android only; this function may be renamed or moved in a future release)
	 *
	 * @param SpecificPlayer Specific player's achievements to show. May not be supported on all platforms. If null, defaults to the player with ControllerId 0
	 */
	UFUNCTION(BlueprintCallable, Category = "Utilities|Platform")
	static void ShowPlatformSpecificAchievementsScreen(class APlayerController* SpecificPlayer);
	
##### Operate System

	/**
	 * Returns whether the player is logged in to the currently active online subsystem.
	 *
	 * @param Player Specific player's login status to get. May not be supported on all platforms. If null, defaults to the player with ControllerId 0.
	 */
	UFUNCTION(BlueprintPure, Category = "Online")
	static bool IsLoggedIn(APlayerController* SpecificPlayer);

	/**
	 * Returns true if screen saver is enabled.
	 *
	 */
	UFUNCTION(BlueprintCallable, Category = "Utilities|Platform")
	static bool IsScreensaverEnabled();

	/**
	 * Allows or inhibits screensaver
	 * @param	bAllowScreenSaver		If false, don't allow screensaver if possible, otherwise allow default behavior
	 */
	UFUNCTION(BlueprintCallable, Category = "Utilities|Platform")
	static void ControlScreensaver(bool bAllowScreenSaver);

	/**
	 * Allows or inhibits system default handling of volume up and volume down buttons (Android only)
	 * @param	bEnabled				If true, allow Android to handle volume up and down events
	 */
	UFUNCTION(BlueprintCallable, Category = "Utilities|Platform")
	static void SetVolumeButtonsHandledBySystem(bool bEnabled);

	/**
	 * Returns true if system default handling of volume up and volume down buttons enabled (Android only)
	 */
	UFUNCTION(BlueprintPure, Category = "Utilities|Platform")
	static bool GetVolumeButtonsHandledBySystem();
	
