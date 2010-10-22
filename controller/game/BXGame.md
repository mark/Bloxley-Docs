# BXGame

_Location_: `bloxley.controller.game.BXGame`

_Superclass_: `bloxley.controler.game.BXInterface`

`BXGame` is the base controller for every game.  It handles managing other controllers, top level interface elements, and saving and loading levels.

_Should you subclass this?_ Yes, every game should contain one `BXGame` subclass.

_Should you instantiate this?_ Yes, in the .fla file itself, you should create an instance of your `BXGame` subclass.

## Constructor

### BXGame(stage:Stage)

Creates a `BXGame` instance, and initializes the clock and mailbox subsystems.  The flash `Stage` object is used to create a root movie clip, which contains all of the game's assets.

## Controller Methods
        
### controllers(classHash:Object)

Pass in a hash mapping controller key name to controller class.  The names are currently only relevant for `BXController` and `BXActorController` subclasses; kinds of controllers are distinguished by their ancestry.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, you definitely need to call this in your constructor.

## Entity Controller Methods

### patchController():BXPatchController

Return the patch controller for the game.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ You probably won't need to, but you could.

### actorControllerForTile(tile:String):BXActorController

Returns the actor controller that will generate an actor on the given board tile, if one exists.  Does not currently handle a situation where a board character would generate multiple, stacked actors.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Probably not; it's used by the level loading system.

## Game Controller Methods
    	
### currentGameController():BXController

Return the currently active game flow controller (subclass of `BXController`).

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ No, there's really no need.

### setCurrentGameController(name:String)

Change the currently active game flow controller to the one named `name`.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, whenever you want to change game modes.  (Usually play <---> edit).

## Event Methods

### respondTo(meth:String, args:Array = null)

This is called by interface elements when they are interacted with.  It resolves the source by looking for what object responds to the method named `meth`.  The order that it looks is:

1. this
2. current game controller

_Should you override this?_ If you want to change the response order, or add something into that list.  But that's a pretty drastic thing to do.

_Should you call this?_ Yes, but from pens or custom interface elements.

## GUI Element Methods
        
### createInterface()

A hook to create top level interface components--ie, components that are visible no matter which game controller is active.  This is mostly the game grid itself, and buttons to switch between game controllers, although any visual details you want to always show should be created in here.  By default, it creates a grid with default grid size as returned by `defaultGridSize()`, and puts it in the interface bank named "Main".

_Should you override this?_ Yes, whenever you want custom top level interface components.

_Should you call this?_ No, it gets called by `BXGame`'s constructor.

### defaultGridSize():Number

Allows you to change the grid size without having to override `createInterface()`.  By default, returns `32.0`.

_Should you override this?_ Sure, if you want to change the grid size.

_Should you call this?_ Maybe, if you override `createInterface()` but still want to use it.

## Board Methods
        
### createBoard()

Creates an instance of `BXBoard` linked to this game, and sets it to be the current board.

_Should you override this?_ Only if you're using a custom subclass of `BXBoard`.

_Should you call this?_ No, this gets called by bloxley when creating levels.

### board():BXBoard

Returns the current board for this game, creating it if it doesn't exist.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, it's useful whenever you want to get board entities.

### setBoard(board:BXBoard)

Sets the board `board` to be the current game board.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ No.

### attachBoardToGrid(board:BXBoard = null, grid:BXGrid = null)

Links the board model object with the grid view object.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ No.

## Grid Methods

### grid():BXGrid

Returns the current `BXGrid` instance for this game.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Possbly, if you want to animate the board in some way.

## Level Methods

### createLevel(width:Number, height:Number, callback:Function)

Create a blank level (ie, every patch is set to the first patch) with the given size, and passes it into the callback function.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, if you want to create a brand new level from scratch.  But probably indirectly, through an gui element that you create.

## Loading Methods

### loadPatch(tile:String, placeX:int, placeY:int):BXPatch

Creates a new patch from the character `tile`, and places it at `(placeX, placeY)` on the board.  Returns the new patch.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ No, the loading methods call this.
        
### loadActorFromBoard(tile:String, location:BXPatch)

Creates a new actor from the character `tile` (if possible), and if so places it at the patch `location` on the board.  Returns the new actor.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ No, the loading methods call this.

### loadLevel(rows:Array, objects:Array = null)

Loads a new level from an array of strings which correspond to the board, and an array of objects, which generate actors that are too complicated to be described on the board.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, if you want to manually generate a level (as opposed to loading it from a server).

## Saving Methods
        
### previousLevel()

Load the previous level in the level sequence from the server.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, but indirectly--through a keyboard command or button.

### nextLevel()

Load the next level in the level sequence from the server.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, but indirectly--through a keyboard command or button.

### saveBoard()

Saves the board onto the server.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, but indirectly--through a keyboard command or button.

