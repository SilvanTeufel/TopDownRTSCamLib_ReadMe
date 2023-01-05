# TopDownRTSCamLib - Readme - 2022

Copyright 2022 Silvan Teufel / Teufel-Engineering.com All Rights Reserved.
For Questions you can write to info@teufel-engineering.com

V 1.X.X is deprecated soon, please switch to Version 2.X.X

## Download the Plugin

https://www.unrealengine.com/marketplace/en-US/product/86b66e1dccc74679abc3e5c3eec2fd2a

If you have downloaded the plugin it can be found in your Unreal Engine folder:
C:\Program Files\Epic Games\UE_5.0\Engine\Plugins\TopDownRTSCamLib (for example)
If you can find this folder in your enginge plugins folder the download was successful.
If the plugin is in another folder, you should copy it here.

## Install the Plugin

Open Unreal Editor. Click Edit -> Plugins to open the plugin window.
Search for TopDownRTSCamLib and put a check mark at it.

## Import Keyboard Settings and Maps and Modes

Download here from Github:

Input Backup 2023-01-04 092036.ini -> Project Settings -> Input -> Import
Maps & Modes Backup 2023-01-04 211553.ini  -> Project Settings -> Maps and Modes -> Import

These files should be also available inside the Plugins Folder in Documents/Inputs


## Test Example Map

Open Unreal Editor. Open folder (In Unreal Editor folder tab):
All\Engine\Plugins\TopDownRTSCamLib\Content\Level\levelOne


## Example Blueprints

Your can find example Blueprints in the Unreal Editor as well:
All\Engine\Plugins\TopDownRTSCamLib\Content\Blueprints

This Blueprints use the Parent Classes from TopDownRTSCamLib Plugin, which you can use for your Blueprints as well.

## Parent Classes

If TopDownRTSCamLib is installed the Classes can be used as Parent Class in Blueprint, so all functions from this Class are available.
Just use one of the following Classes as Parent Class and or just choose them in your GameMode Blueprint. Category = TopDownRTSCamLib

Parentclasses are:

- CameraBase
- CharacterBase
- HUDBase
- ControllerBase
- SelectedCharacterIcon

For CameraBase, if you want only to use the Functions and not run the Code in Tick and BeginPlay (which is automatically setup), just set the Variables to true:

- DisableTick
- DisableBeginPlay

For ControllerBase, if you want to use the Controller, you have to adapt your Settings (Pictures in "Document/Inputs" Folder), or import the 
"Input Backup 2023-01-04 092036.ini" and "Maps & Modes Backup 2023-01-04 211553.ini" inside the "Inputs" Folder, or download from Github.
You also have to set Lock Viewport on Mouse as "always".

---

Here you can find the Classes with Porperties and Functions (V2.X.X - is in Work):


# CameraBase

|CameraState (The Statemachine is used in CamerControllerBase)        	|Note                         |
|---------------------------------------------------------------|-----------------------------|
|UseScreenEdges     UMETA(DisplayName = "UseScreenEdges")       | CharAnimState = UseScreenEdges  |
|MoveForward  UMETA(DisplayName = "MoveForward"),    		| CharAnimState = MoveForward |
|MoveBackward   UMETA(DisplayName = "MoveBackward"),    	| CharAnimState = MoveBackward |
|MoveLeft   UMETA(DisplayName = "MoveLeft"),      		| CharAnimState = MoveLeft |
|MoveRight   UMETA(DisplayName = "MoveRight"),			| CharAnimState = MoveRight |
|ZoomIn  UMETA(DisplayName = "ZoomIn"),     		        | CharAnimState = ZoomIn  |
|ZoomOut  UMETA(DisplayName = "ZoomOut"),  			| CharAnimState = ZoomOut  |
|ZoomOutPosition  UMETA(DisplayName = "ZoomOutPosition") ,     	| CharAnimState = ZoomOutPosition  |
|ZoomInPosition  UMETA(DisplayName = "ZoomInPosition"),   	| CharAnimState = ZoomInPosition |
|RotateLeft UMETA(DisplayName = "RotateLeft"),               	| CharAnimState = RotateLeft  |
|RotateRight UMETA(DisplayName = "RotateRight"),              	| CharAnimState = RotateRight |
|LockOnCharacter UMETA(DisplayName = "LockOnCharacter"),      	| CharAnimState = LockOnCharacter |
|ThirdPerson UMETA(DisplayName = "ThirdPerson"),                | CharAnimState = ThirdPerson  |
|ZoomToThirdPerson UMETA(DisplayName = "RotateBeforeThirdPerson"), | CharAnimState = ZoomToThirdPerson |


|Properties (EditAnyWhere + BlueprintReadWrite)                  	|Note                         |
|-----------------------------------------------------------------------|-----------------------------|
|USceneComponent* RootScene;         				        | The RootScene      						|
|USpringArmComponent* SpringArm;          				| The SpringArm         					|
|FRotator SpringArmRotator = FRotator(-50, 0, 0);			| Used to rotate the SpringArm in Constructor			|
|UCameraComponent* CameraComp;        					| The CameraComponent         					|
|APlayerController* PC;          				        | Is Pointing to the ControllerBase (Parent of CameraControllerBase) |
|float CameraDistanceToCharacter;					| Is used to Hold the Camera Distance to Character when Cam is locked to Chararcter |
|float Margin = 30;      				                | Distance to Screenedges where Edgescrolling should start	|
|int32 ScreenSizeX;           				                | Is set in BeginPlay of CamControler by  GetViewPortScreenSizes() |
|int32 ScreenSizeY;         					        | Is set in BeginPlay of CamControler by  GetViewPortScreenSizes() |
|int GetViewPortScreenSizesState = 1;      				| 1 is for Viewport 2 for System Resolution - used in GetViewPortScreenSizes() |
|float CamSpeed = 80;		                                        | Choose a Multiplier for the CamSpeed	|
|float ZoomOutPosition = 20000.f;	                                | STRG + HOLD Space Position |
|float ZoomPosition = 1500.f;         			                | Normal RTS-Cam Distance |
|float ZoomThirdPersonPosition = 600.f;      				| Distance to Character in Third Person |
|float CamRotationOffset = 11.5f;                                 	| Is used when Rotating around Character. This Offset Moves the Cam in x/y while rotating |
|float CameraAngles[4] = { 0.f, 90.f, 180.f, 270.f };		        | Choose a for CamAngles where the Camera should stop, when rotating |
|class UWidgetComponent* ControlWidgetComp;		       		| Choose a controll Widget |
|FRotator ControlWidgetRotation = FRotator(50, 180, 0);	        	| Choose a Rotation for the Widget |
|FVector ControlWidgetLocation = FVector(400.f, -350.0f, -250.0f);	| Choose a Location for the Widget |
|Vector ControlWidgetHideLocation = FVector(400.f, -2500.0f, -250.0f);	| Choose a Hidden Location for the Widget |
	

|Properties (BlueprintReadWrite)                  		|Note                         |
|---------------------------------------------------------------|-----------------------------|
| float YawValue = 0.f;        					| Of the Camera / SetControlrotation to Rotate       |
| float PitchValue = 0.f;					| Of the Camera / SetControlrotation to Rotate       |
| float RollValue = 0.f;       					| Of the Camera / SetControlrotation to Rotate       |
| RotationDegreeStep        					| Used for Rotation	             |

	
|Functions (BlueprintCallable)                  		|Note                         |
|---------------------------------------------------------------|-----------------------------|
|void CreateCameraComp();			   		| Created the CameraComp, called in Constructor |
|void SpawnControllWidget();     				| Spawns the Controll Widget           |
|void PanMoveCamera(const FVector& NewPanDirection);      	| Used for Edge scrolling inside the Tick |
|void ZoomIn();						       	| Zoom Camera In |
|void ZoomOut();						| Zoom Camera Out |
|void ZoomStop();     						| Stops Zoom 					|
|void CamLeft();      						| Moves Cam Left				|
|void CamRight();      						| Moves Cam Right				|
|bool RotateCamLeft(bool UseCamRotationOffset);   		| Changes YawValue for Left Rotation. SetControlRotation has to be called after.|
|bool RotateCamRight(bool UseCamRotationOffset);      		| Changes YawValue for Right Rotation. SetControlRotation has to be called after.|
|bool RotateCamLeftTo(float Position);    			| Changes YawValue +=1 till "Position" is reached          	|
|bool RotateCamRightTo(float Position);       			| Changes YawValue -=1 till "Position" is reached          	  |	
|void JumpCamera(FHitResult Hit);      				| Jump Camera to Hit Position.			          	  |	
|FVector2D GetMousePos2D();      				| Gets Mouse Position via Controller |	
|void Zoom();       						| Zooms the Camera          	  |	
|void ZoomOutToPosition(float Distance, const FVector SelectedActorPosition = FVector(0.f,0.f,0.f)); | Zoom to Distance |	
|bool ZoomInToPosition(float Distance, const FVector SelectedActorPosition = FVector(0.f,0.f,0.f)); | Zoom to Distance |	


Here you can find the Classes with Porperties and Functions ( V1.X.X):

### Class - CameraBase

```
void CreateCameraComp();

USceneComponent* RootScene;

USpringArmComponent* SpringArm;

FRotator SpringArmRotator = FRotator(-50, 0, 0);

 UCameraComponent* CameraComp;

 APlayerController* PC;

 void GetViewPortScreenSizes(int x);

 void SpawnControllWidget();

- Functionality is defined by Functionname

FVector GetCameraPanDirection();

void PanMoveCamera(const FVector& PanDirection);

- Scrolling with Screen Edges This is Called in Tick generaly with CamSpeed: PanMoveCamera(GetCameraPanDirection() \* CamSpeed);

float Margin = 15;

int32 ScreenSizeX;

- Screen Edge For Scrolling with Mouse

int32 ScreenSizeY;

- Screen Edge For Scrolling with Mouse

int GetViewPortScreenSizesState = 1;

- Set 2 for System Resolution, Set 1 for Viewport Edges
- The Function Defines ScreenSize X and Y

float CamSpeed = 80;

- Camspeed for Scrolling with Screen Edges

void ZoomIn();

- Functionality is defined by Functionname

void ZoomOut();

- Functionality is defined by Functionname

void ZoomStop();

- Functionality is defined by Functionname

void CamLeft();

- Functionality is defined by Functionname

void CamRight();

- Functionality is defined by Functionname

void CamStop();

- Functionality is defined by Functionname

void CamRotationTick();

- Is Used For Rotation is generaly called in Tick

void JumpCamera(FHitResult Hit);

- Jump Camera to Hit Position

FVector2D GetMousePos2D();

- Functionality is defined by Functionname

void Zoom();

- Functionality is defined by Functionname

void ZoomOutToPosition();

- Functionality is defined by Functionname

void CamMoveAndZoomTick();

- For Cam Movement and Cam Zoom generaly called in Tick

void ZoomInToPosition();

- Sets ZoomCamOutToPosition to true

void LockOnCharacter(ACharacter\* SelectedActor);

- Lock the Camera to an Actor, ZoomCamOutToPosition is checked

float ZoomOutPosition = 20000.f;

- Cameraposition when ZoomOutToPosition() is called.

float ZoomPosition = 1500.f;

- Cameraposition when ZoomInToPosition() is called.

float PitchValue = 0.f;

- Of the Camera

float YawValue = 0.f;

- Of the Camera

float RollValue = 0.f;

- Of the Camera

bool RollCamRight = false;

- Functionality is defined by Functionname

bool RollCamLeft = false;

- Functionality is defined by Functionname

bool ZoomCamOut = false;

- Functionality is defined by Functionname

bool ZoomCamIn = false;

- Functionality is defined by Functionname

bool ZoomCamOutToPosition = false;

- Functionality is defined by Functionname

bool MoveCamForward = false;

- Functionality is defined by Functionname

bool MoveCamBackward = false;

- Functionality is defined by Functionname

bool MoveCamLeft = false;

- Functionality is defined by Functionname

bool MoveCamRight = false;

- Functionality is defined by Functionname

float startTime = 0.f;

- Functionality is defined by Functionname

int CamAngle = 0;

- Should not be changed. Is to keep Track of actual Angle

bool DisableTick = false;

- Disable My Tick Functions of Parent Class, to use my Function in Blueprint

bool DisableBeginPlay = false;

- Disable BeginPlay Functions of Parent Class, to use my Function in Blueprint

class UWidgetComponent\* ControlWidgetComp;

- Keyboard Widget (which is shown by pressing Tab)

FRotator ControlWidgetRotation = FRotator(50, 180, 0);

- Rotation of The Widget

FVector ControlWidgetLocation = FVector(400.f, -350.0f, -250.0f);

- Location of the Widget when shown

FVector ControlWidgetHideLocation = FVector(400.f, -2500.0f, -250.0f);

- Location of the Widget when hidden

void HideControlWidget();

- Functionality is defined by Functionname

void ShowControlWidget();

- Functionality is defined by Functionname

```

---

### Class - HUDBase

```
virtual void DrawHUD();

- Used in Tick() to Draw the Selectionfield and trigger select.

FVector2D InitialPoint;

- Position of mouse on screen when pressed;

FVector2D CurrentPoint;

- Position of mouse on screen while holding;

float RectangleScaleSelectionFactor = 0.9;

- Factor of inner/outer selection field

FVector2D GetMousePos2D();

- Functionality is defined by Functionname

void AimToMouse();

- Actors can be triggert to Look to the Mouse

void MoveActorsThroughWayPoints(TArray <ATopDownExampleCharacter\*> Actors);

- Move Actors through Waypoints

void StartMovingActors(TArray<ATopDownExampleCharacter\*> Actors);

- Start Move Actors.

void setZeroActor(ATopDownExampleCharacter\* Actor);

- Functionality is defined by Functionname

bool bStartSelecting = false;

TArray <ATopDownExampleCharacter\*> FoundActors;
```
---

### Class - ControllerBase

```
void ShiftPressed();

void ShiftReleased();

void LeftClickPressed();

void LeftClickReleased();

void RightClickPressed();

void SpacePressed();

void SpaceReleased();

void QPressed();

void WPressed();

void APressed();

void AReleased();

void JumpCamera();

void StrgPressed();

void StrgReleased();

void ZoomIn();

void ZoomOut();

void ZoomStop();

void CamLeft();

void CamRight();

void ControllDirectionToMouse(ATopDownExampleCharacter\* SelectedActor);

void ToggleLockCameraToCharacter();

void TabPressed();

void TabReleased();

void CameraPawnForward();

void CameraPawnBackward();

void CameraPawnLeft();

void CameraPawnRight();

void CameraPawnForwardR();

void CameraPawnBackwardR();

void CameraPawnLeftR();

void CameraPawnRightR();

bool IsShiftPressed = false;

bool AIsPressed = false;

bool IsStrgPressed = false;

bool IsSpacePressed = false;

bool LockCameraToCharacter = false;

TArray <ATopDownExampleCharacter*> SelectedActors;

TArray <ATopDownExampleCharacter*> MovingActors;
```
