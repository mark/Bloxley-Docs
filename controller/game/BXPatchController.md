# BXPatchController

_Location_: `bloxley.controller.game.BXPatchController`

_Superclass_: `bloxley.base.BXObject`

`BXPatchController` is the superclass for all patch controllers.  It handles loading & saving patches, displaying them, and their behaviors.

_Should you subclass this?_ Yes, you need to create a subclass to define your patches.

_Should you instantiate this?_ No, bloxley will instantiate this, but you need to tell bloxley about it by calling `BXGame#controllers` in your custom game subclass's constructor.

## Constructor

### BXPatchController(name:String, game:BXGame)

## Tile Library Methods

### tile(key:String, xmlChars:String, frame:String = null)

Define a tile--the characters in `xmlChars` all correspond to a patch of **key** `key`.  You can provide a frame name to use for this kind of patch, but by default it is "key".

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, you need to call either this (repeatedly) or `tiles()` to define your game's patches.

### tiles(object:Object)

Define a set of tiles.  `object` is iterated over--the keys become the patch **keys**, and the values because the characters that correspond to a patch of that type.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, you need to call either this or `tile()` repeatedly to define your game's patches.

### library():BXTileLibrary

Returns the tile library for this controller.  The tile library keeps track of defined tiles.

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ No, bloxley calls this method internally.

## Creation Methods
        
### createPatch(char:String)

### initializePatch(patch:BXPatch)

## Sprite Attribute Methods
        
### graphicsName(patch:BXPatch):String

### frameName(patch:BXPatch):String

### registrationAtCenter(patch:BXPatch):Boolean

## Sprite Methods      
        
### spriteForPatch(patch:BXPatch):BXSprite
    
### renderPatchSprite(patch:BXPatch, sprite:BXCompositeSprite):BXCompositeSprite
        
        // Set it to the correct clip and frame
### displaySprite(patch:BXPatch, sprite:BXCompositeSprite)


### resizeSprite(patch:BXPatch, sprite:BXSprite)
            // Resize the sprite to the current screen size...

        
### initializeSprite(patch:BXPatch, sprite:BXSprite) 
    		// OVERRIDE ME!

## Event Methods

### resolveEvent(action:BXAction, eventType:String, source:BXActor, target:BXPatch):Boolean

## Default Event Handlers

### canEnter(action, source:BXActor, target:BXPatch)

### canExit(action, source:BXActor, target:BXPatch)

## Saving Methods

### exportPatch(patch:BXPatch):String
