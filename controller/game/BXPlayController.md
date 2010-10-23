# BXPlayController

         BXPlayController(name: String, game:BXGame)

        /*************************
        *                        *
        * Initialization Methods *
        *                        *
        *************************/
        
         onStart()

         createInterface()

         createPens()

    	 createPhases()

    	/****************
    	*               *
    	* Phase Methods *
    	*               *
    	****************/
    	
    	 setInitialPhase(phaseName:String)

    	// This contains the built in game loop, useful for Sokoban-type games
    	// But not useful for more complex kinds of games.
    	// Override when necessary...
    	 phase(name:String, options:Object = null):BXPhase
    	
        /********************
        *                   *
        * Monitoring Events *
        *                   *
        ********************/
        
         startMonitoringEvents()
        
         fetchEvents():Array
        
         pushEvents()

         startMonitoringUserEvents(events:Array)
        
         finishMonitoringUserEvents()
        
         respondTo(meth:String, args:Array = null)
        
         eventSucceeded(event:BXEvent):BXRoutine

        /***************
        *              *
        * Undo Methods *
        *              *
        ***************/
        
         undo()

         reset()
        
    	/*************************
    	*                        *
    	* Built-In Phase Methods *
    	*                        *
    	*************************/

    	 startGame()
    	
    	// These are the user input actions which will trigger a phase transition
    	 validUserActions():Array
    	
    	 heartbeat()
    	
    	 didBeatLevel():Boolean

    	 beatLevel()

    	 didLoseLevel():Boolean

    	 lostLevel()
    	
    	/*****************************
    	*                            *
    	* Built-In Animation Methods *
    	*                            *
    	*****************************/
    	
    	 animateBeatLevel(action:BXAction)
    	
    	 animateUndoBeatLevel(action:BXAction)
    	
    	 animateLostLevel(action:BXAction)

    	 animateUndoLostLevel(action:BXAction)
    	
    	/****************
    	*               *
    	* Timer Methods *
    	*               *
    	****************/

    	 setupTimer()

    	 initialize(message:BXMessage)

    	 everyFrame(message:BXMessage)

    	 everySecond(message:BXMessage)

        /*******************
        *                  *
        * Gameplay Methods *
        *                  *
        *******************/
        
         selectPlayer(character:BXActor)
        
         selectNextPlayer()
        
         moveCharacter(direction:BXDirection, steps:int = 1)
