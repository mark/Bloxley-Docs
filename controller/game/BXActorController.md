# BXActorController

_Location_: `bloxley.controller.game.BXActorController`

_Superclass_: `bloxley.base.BXObject`

`BXActorController` is the superclass for all actor controllers.  It handles loading & saving actors, displaying them, and their behaviors.

_Should you subclass this?_ Yes, you should create a subclass for each kind of actor that your game contains.

_Should you instantiate this?_ No, bloxley will instantiate this, but you need to tell bloxley about it by calling `BXGame#controllers` in your custom game subclass's constructor.

## Constructor

### BXActorController(name:String, game:BXGame)

## Getters and Setters

### board():BXBoard

Return the board that this controller's actors are placed on.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes.

## Actor Attribute Methods

### key(options = null):String

Return the key for the actor which will be created with the given options.

_Should you override this?_ Yes, you have to.  Every actor needs to have a key.

_Should you call this?_ No, bloxley calls it when instantiating objects.

### canBePlayer(actor:BXActor):Boolean

Can the given actor be a player (ie, be directly controlled by the user).  `BXPlayPen` and its subclasses look for actors that can be player.  By default it always returns false.

_Should you override this?_ Yes, if there's a possibility that one of this controller's actors can be a player.

_Should you call this?_ Not really.  You can call it indirectly through `BXGroup` methods, but there's no need to call it directly.

### isGood(actor:BXActor):Boolean

A generic predicate for actors that hooks into methods in `BXGroup`.  Commonly used for determining the end of the game.  By default it always returns false.

_Should you override this?_ If you want it to mean something.  Probably only for the one or two kinds of actors that are used to determine when the level is over.

_Should you call this?_ Not really.  You can call it indirectly through `BXGroup` methods, but there's no need to call it directly.

### regionForActorAtLocation(actor:BXActor, location:BXPatch):BXRegion

Generates the `BXRegion` that the actor `actor` occupies when located at `location`.  By default, simply returns the single patch region containing `location`.

_Should you override this?_ Only for actors that occupy more than one patch at a time.

_Should you call this?_ No.

### regionForActor(actor:BXActor):BXRegion
        
Returns the region that the actor `actor` currently occupies.  Regenerates it if `actor` has moved.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Possibly, but more likely it will be called by `BXRegion` methods.

## Creation Methods        

### createActor(options):BXActor

Creates an instance of `BXActor` with the given options.

_Should you override this?_ Only if you're going to use a custom `BXActor` subclass.  Which is rarely necessary.

_Should you call this?_ No.

### createActorFromBoard(tile:String):BXActor

Creates an instance of an actor from the character given.  Returns `null` if the character doesn't correspond to this kind of actor.

_Should you override this?_ No.

_Should you call this?_ No.

### initializeActor(actor:BXActor)

A hook to perform any desired setup for new actors.  By default it doesn't do anything.

_Should you override this?_ If you want to perform any setup on this kind of actor.  Usually not.

_Should you call this?_ No.

## Sprite Attribute Methods

These methods are used to create the sprite for an actor.  Thus, they are only called at the start of the game--later changes to the actor's sprite must be done through animations.

### graphicsName(actor:BXActor):String

Returns the class name for the kind of movie clip to use to display the given actor.  If you return `Foo`, then bloxley will call `new game.Foo()` for the sprite.  By default it just returns the actor's key.

_Should you override this?_ Probably not.  Having the graphic name and the key being the same keeps things consistent.

_Should you call this?_ No.

### frameName(actor:BXActor):String

Returns the name of the frame to display for the given actor's sprite.  By default, it returns `null`, which makes bloxley display the movie clip's first frame.

_Should you override this?_ Yes, if you have multiple frames for the actor, and need to display a particular one.

_Should you call this?_ No.

### dimensions(actor:BXActor):Array

Returns a `[length, width]` pair corresponding to how big the actor `actor` should appear on-screen (1 patch = 1.0).  By default returns `[1.0, 1.0]`.

_Should you override this?_ Only if the actor's sprite shouldn't take up exactly one patch.

_Should you call this?_ No.

### registrationAtCenter(actor:BXActor):Boolean

Is the registration point for the sprite's movie clip in the center (as opposed to the top left corner).  By default returns `false`.

_Should you override this?_ Only if the actor's sprite is centered around the registration point.  This is useful for when the sprite's dimensions aren't `[1.0, 1.0]`.

_Should you call this?_ No.

## Sprite Methods

### spriteForActor(actor:BXActor):BXSprite

Returns the sprite for the actor `actor`.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, it's frequently necessary.

### renderActorSprite(actor:BXActor, sprite:BXCompositeSprite):BXCompositeSprite

Generates a sprite for the actor `actor`.  It takes in an empty `BXCompositeSprite`, and inserts the sprite's movie clip.  This is called when the sprite is first generated.  This returns the movie clip as well, to allow method chaining.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ No.

### displaySprite(actor:BXActor, sprite:BXCompositeSprite)

Sets the sprite `sprite` to the correct clip and frame, by calling `graphicsName()` and `frameName()`.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ No.

### resizeSprite(actor:BXActor, sprite:BXSprite)

Resize the sprite `sprite` to the correct screen size, by calling `dimensions()`.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_

### initializeSprite(actor:BXActor, sprite:BXSprite) 

A hook to allow any custom sprite initialization to be performed.  By default it does nothing.

_Should you override this?_ Yes, if you want to modify the sprite at all when it is created.

_Should you call this?_ No.

## Event Methods        

### resolveEvent(action:BXAction, eventType:String, source:BXActor, target:BXActor):Boolean

Attempts to handle an action performed on the actor `actor`.  Return true if the event succeeded, false if it did not.  Uses method cascading to call a series of increasingly general methods as follows:

1. `can (eventType) (target's key)`
2. `can (eventType)` -- this method is always defined.

`eventType` is one of `StepOn`, `BeSteppedOnBy`, `Leave`, `BeLeftBy`.

## Default Event Handlers

### canStepOn(action:BXAction, source:BXActor, target:BXActor)

This is the active form of the event for when one actor (the `source`) moves onto a patch occupied by another actor (the `target`).  This is the most general event handler, so it is always defined.  Call `succeed()` or `fail()` on the action.  By default, allows the action to succeed.

_Should you override this?_ Probably not; in most cases you want to define a more specific event handler.  However, it is possible, just make sure you always call `action.succeed()` or `action.fail()`

_Should you call this?_ No, this is called by bloxley's event system.

### canBeSteppedOnBy(action:BXAction, source:BXActor, target:BXActor)

This is the passive form of the event for when one actor (the `source`) has another actor (the `target`) move onto a patch it occupies.  This is the most general event handler, so it is always defined.  Call `succeed()` or `fail()` on the action.  By default, it causes the action to fail, preventing actors from overlapping.

_Should you override this?_ Possibly, if you want all other actors to be able to move onto this controller's actors.  Usually, you want to define a more specific event handler for cases where this is possible.  If you do redefine this, just make sure you always call `action.succeed()` or `action.fail()`

_Should you call this?_ No, this is called by bloxley's event system.

### canLeave(action:BXAction, source:BXActor, target:BXActor)

This is the active form of the event when one actor (the `source`) moves off the the patches occupied by another actor (the `target`).  This is the most general event handler, so it is always defined.  Call `succeed()` or `fail()` on the action.  By default, allows the action to succeed.

Generally, this is used to perform actions when an actor is stepped off.

_Should you override this?_ Possibly, if you want to prevent an actor from being stepping off, or if you want to define an action that occurs when it steps off.  Usually, you want to define a more specific event handler for these cases.  If you do redefine this, just make sure you always call `action.succeed()` or `action.fail()`

_Should you call this?_ No, this is called by bloxley's event system.

### canBeLeftBy(action:BXAction, source:BXActor, target:BXActor)

This is the passive form the the even when one actor (the `source`) has another actor (the `target`) move off of the patches that it occupies.  This is the most general event handler, so it is always defined.  Call `succeed()` or `fail()` on the action.  By default, it causes the action to succeed.

_Should you override this?_ Possibly, if you want to prevent an actor from being stepped off, or if you want to define an action that occurs when it is stepped off.  Usually, you want to define a more specific event handler for these cases.  If you do redefine this, just make sure you always call `action.succeed()` or `action.fail()`

_Should you call this?_ No, this is called by bloxley's event system.

## Default Animations

### defaultSpeed(...args):Number

Returns the default movement speed for animating this sprite when it moves around.  Used by the default implementation of `animateMove()`.  Measured in patches per second.  By default, it returns `8.0`.

_Should you override this?_ If you want a different default speed for your animations.

_Should you call this?_ You can, if you override `animateMove()` but still want to use this method.  Not really necessary, though.

### animateMove(actor:BXActor, action:BXMoveAction, instant:Boolean = false)

Returns the animation when the actor `actor` is moved by the action `action`.  By default, it just returns a `BXSprite#goto` animation.

_Should you override this?_ If you want a more interesting animation than the sprite sliding around.

_Should you call this?_ No, this is called by a choreographer.

### animateSelect(actor:BXActor, action:BXSelectAction)

Returns the animation when the actor `actor` is selected by the action `action`.  By default, it does nothing.

_Should you override this?_ If you want to animate when an actor is selected.  Which you probably do.

_Should you call this?_ No, this is called by a choreographer.

## Representation Methods

### setBoardString(boardString:String)

Tells the controller what characters on the board should be used to generate actors of this controller's type.  Pass in a string with all the possible characters.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, if your actors are simple enough to show up on the board directly.  Call it in the constructor.  Don't call both this and `attributes()`.

### attributes(attributeHash:Object)

Tells the controller what kind of XML tags this actor contains, and their type.  Pass in a hash `{ tag: type}`, where `type` is one of: `'Number'`, `'Boolean'`, `'Color'`, `'String'`, or `'Direction'`.  Also, by passing in `location: false`, the actor will not be placed on the board.  To be honest, I don't remember what that's useful for.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ Yes, if your actors are more complicated than a single character easily describes.  Call it in the constructor.  Don't call both this and `setBoardString()`.

## Loading Methods

### canLoadFromBoard(tile:String):Boolean

Can an actor of this type be loaded from the single character `tile`?  Basically, does `tile` appear in the board string passed into `setBoardString()`?

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ No.

## Saving Methods

### includeOnBoard(actor:BXActor)

The converse of `canLoadFromBoard()`, should this actor be placed on a board when saving, or should it get its own XML tag?  Returns true if the board string was set, false if the attribute hash was.

_Should you override this?_ No, most methods depend on it working the way it does.

_Should you call this?_ No.

## Utility Methods

### getDescriptionString(actor:BXActor):String

Returns a string describing the actor.

_Should you override this?_ Yes, every class should define this however it wants.

_Should you call this?_ Sure, for testing and debugging purposes.