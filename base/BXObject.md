# BXObject

_Location_: `bloxley.base.BXObject`

`BXObject` is the superclass for all significant Bloxley classes.  It contains methods for message passing, method cascading, and reflection.

_Should you subclass this?_ Yes, any time you create a new class that you want to have access to bloxley's features

_Should you instantiate this?_ No, this class doesn't do anything on its own.

## ID Methods

### id():int 

Every instance of BXObject gets a unique id number.  This method returns that number.

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ Yes, any time you want an easy way to recognize a unique `BXObject`.

## Mailbox Methods

### listenFor(message:String, source:BXObject, fcn) 

When the object `source` posts a message `message` to the mailbox, call `fcn` on this object. `fcn` can be a fcntion object, or the string name of a method that the caller responds to.

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ Yes, any time you want to observe a particular message.

### listenForAny(message:String, fcn) 

When _any_ object posts a message `message` to the mailbox, call 'fcn' on this object. `fcn` can be a fcntion object, or the string name of a method that the caller responds to.

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ Yes, any time you want to observe a particular message.

### post(message:String, info = null) 

Post a message to the mailbox, optionally with some additional information

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ Yes, when you want to post a message.

### postLater(message:String, seconds:Number, info = null) 

In `seconds` seconds, post the message `message` to the mailbox, optionally with some additional information.

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ Yes, when you want to post a message at some point in the future.

### later(fcn, info:Object = null) 

Later this frame, call the provided method. `fcn` can be a fcntion object, or the string name of a method that the caller responds to.

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ Yes, when you want a method to be called, but after the current call chain resolves.

### stopListening(...rest) 

Remove this object from the mailbox, preventing it from receiving any more messages

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ Yes, when you're ready for this object to be garbage collected.

### recordListeningFor(message) 

Record that this object is listening for a particular message

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ No, bloxley calls this method internally.

### messagesListeningFor():Array 

What messages are this object listening for?

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ No, bloxley calls this method internally.

### recordListenedTo(message) 

Record that some object is listening for a particular message from this object.

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ No, bloxley calls this method internally.

### messagesListenedTo():Array 

What messages are objects waiting for from this object?

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ No, bloxley calls this method internally.

## Cascading Methods

### callCascade(meths:Array, args:Array = null) 

Given a list of methods (provided as strings), it will find the first that this object responds to, and call it on this object, returning the result.

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ Maybe?  bloxley uses it internally but it can be useful in particular circumstances.

### callResolve(meth:String, objects:Array, args:Array = null) 

Given a method and an array of objects, it will call the method named `meth` on the first object that responds to it, returning the results.

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ Maybe?  bloxley uses it internally but it can be useful in particular circumstances.

## Reflection Methods

### respondsTo(method:String):Boolean

Does this object have a method named `method`?

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ Sure.

### className():String 

What is the name of this class?

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ Sure.

### klass():Class 

What is the class object that this is an instance of?

_Should you override this?_ No, most classes depend on it working the way it does.

_Should you call this?_ Sure.

## Utility Methods

### toString():String 

Return a string description of this object.
 
_Should you override this?_ Yes, every class should define this however it wants.

_Should you call this?_ Sure, for testing and debugging purposes.
 