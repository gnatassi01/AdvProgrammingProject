# AdvProgrammingProject
-Gatphan Atassi and Brendan Kearney-
This file explains the workings of this project.
All relevant files are in the src directory (except for the eventFileUpdated file containing events information [a text file])

Contained in this src file are 3 components' files:
>eventBuilder: interactive gui that can create, modify,or delete choices for events and ultimately save them to a text file that feeds the game event information
  >run via running EventBuilder.java
  >requires SpringUtilities.java to provide the gui layout
>eventObject: This file contains 2 components
  >EventObject.java: this stores an event's information including name, descrption, and three choices(with their respective data)
  >EventReader.java: this program takes the file evenFileUpdated and returns to the caller (in this case the game initializer) an complex array of length 4. This array corresponds to the 4 times of day per day represented in the game. Each array element is a list of EventObjects. TLDR: the first element of the returned array is a list of all EventObjects that occur during the morning time slot
>mainEngine: This is where everything involving the game's running goes. there are 5 components
  >ProjectRunner.java: ***To run the game, run this file.*** This sets up everything the game needs to operate including the gui, the StatsThread, calling the EventReader, and ultimately creating and launching the game object itself: ThePandemicGame
  >ThePandemicGame.java: This file handles the game logic that ticks over the times of day in a week and the days of the single week duration of the game. This file also interprets choices relayed from the GameWindow(which relays that button x has been pressed) and thus converts choice x's information into another object called a StatRequest. This StatRequest is sent off to the StatThread via an ArrayBlockingQueue
  >StatRequest.java: all elements of a choice's numbers including population(the number of people at the event), density(of the people at the event), covid rate(current covid rate for Mecklenburg County). StatRequests are generated by ThePandemicGame then sent via an ArrayBlockingQueue to the StatThread to be unpacked and handled
  >StatThread.java: This thread, separate from the game operations handles all math and statistics from the choices made. Certain elements from the choices are randomized along a normal distribution to provide more randomness between games (sometimes populations at an event are higher/lower). The StatThread also handles the probabilities of an encounter with an individual and determined whether or not the individual is covid positive. Additionally, there is another randomness factor invloved in whether the individual is wearing a mask or not. I arbitrarily chose that an individual is wearing a mask 70% of the time. The thread will track if the player contracts covid-19, how many people the player came into contact with, how many people the player came into contact with who had Covid, and how many people the player got infected with covid if the player indeed contracted covid. 
  >GameWindow.java: this file sets up the GUI and relays inputs from the buttons to ThePandemicGame while also taking input from the game to push new button text and new text for the scrolling text area
  
Some Notes:
  >This game sorely lacks more events and probably needs more creative people than us.
  >Our events may be too tame. We are limiting a person to 4 opportunities to "do things" during a day which isnt really realistic
  >We want to give each event more statistics but felt that it could not be paralleled for all events
  >After doing this, I felt that maybe 1 week is too short a period to get a true grasp on spreading and contracting Covid. ie the sample size isnt really big enough
  >Upon the end of the last day (day 7) the game immediately asks the StatThread for numbers without checking if the thread still had work to do. This fix is fairly simple but was realized after the fact.
  >Possible expansion in the future is asking the player for their location and using the location to get a specific covid rate for the game.
  
 Task management:
 EventBuilder: Brendan
 EventObject: Gatty
 EventReader: Brendan
 ProjectRunner: Gatty
 ThePandemicGame: Gatty
 StatRequest: Gatty
 StatThread: Gatty
 GameWindow: Gatty
 eventFileUpdated (the research and most of the writing): Brendan
