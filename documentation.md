This is your personal wiki page. Only your team and course instructors (TAs and CIs) can see it. You can modifiy this page, upload files to it, or create new pages so long as their names are preceded by "cd016:" (look at the URL of this page; you will see it is prefixed in the same way)

==== TA Notes ====
[[cd016:TA feeadback]]
 mohamed.elgammal@mail.uto




===== Milestone 3 =====

==== Workflow from March 19 to 22 ====

|              ^March 19 ^ March 20 ^March 21 ^ March 22 ^
^ Chaohe Li    |  Setting up of the project.Assign tasks to team members.finish functions for computing travel time and computing walking time      | start working on walk to pick up function(Thinking about algorithm using A* heurstics)| debugging for uber pool function try to use find intersection between paths algorithm and implement into walk and path pick up function   |debugging for uber pool function and working on user inteface  |   | 
^ Jackson Nie  |Set up the project. Assigned tasks to each other.  |Completed basic user guidance ui as well as attempted djikstra algorithm using intersection ids. Found path using djikstra's algorithm but the path was long and tedious| Thought of mechanisms to determine how to find the best path for uber pool function, decided to look through each intersection first|Implemented uber pool by looping through every intersection, finding the path travel time, and comparing to find the fastest route. Passed a few functionality tests but timed out on performance.|
^ Ryan Chang   |Refactor Code to have Global.h so some global variables could be shared between files.Modelling Nodes for Djikstra as Intersections and setting up model | Initial Implementation of Djikstra and A*.At this point, a lot of the cases passed, however I realized that we did not account for turn_penalty when estimating the travel time        |  Try to implement a different model, in which all intersections would be split up into multiple intersections for each unique streetID connected to it. These sub intersections would be connected by made-up streetsegments where the cost would the turn_penalty.   |Debugging new version. Implement UI for clicking on two points of the map to draw the path, used for debugging, changes can be seen on old branches|
==== Workflow from March 23 to 26 ====

|              ^March 23 ^ March 24 ^March 25 ^ March 26 ^
^ Chaohe Li    |  Debugging on passing all of the performance tests      | working on user inteface(basic features) | highlighting path when users choose to select drive function(add icons on the map to make it more distinct)   |make the user interface more interactive and more usable,also final checking code make sure no wanrings are left and deleteing all useless old comments together   |   |  
^ Jackson Nie  | Continued debugging walk drive but still wasn't able to pass performance test     | Started implementing ui as Ryan managed to pass all tests for walk drive using a different approach. Implemented find intersection id by partial intersection name so that the user wouldn't have to type in the intersection id and could use intersection names instead.     |Implemented the highlight algorithm to highlight the found paths for walk and drive. Debugged an error which made the program crash in walk and drive.| Improved the input mechanism for ui which now doesn't contain any duplicates and the asks the user for starting point until one match is found, then asks for ending point, instead of asking for both at the same time then printing all matches for both. Made code warning free and deleted useless comments|                 
^ Ryan Chang   |Went back to intial implementation because new model didn't pass tests, added turn_penalty costs. Pass most of the tests|Implemented find path with walk, passed all of the tests|Debugging last two exercise test cases, figured out a corner case by drawing out everything. Change code to pass all tests cases. Clean up code and added comments| Revert from A* back to Djikstra because A* couldn't pass Very Hard Perf Toronto Inter Inter. At this point, all tests were passed. Synchronize drawing between clicking for paths, typing in two intersections, and walk and driving|

==== Description of Functions====

**Two functions (finding travel time) are done by Chaohe Li **

**Find Path Between Intersections: The first major function find path between intersections are done mostly by Ryan (all memebers participate into giving valuable ideas) **
  * Implementation: Representing all nodes of Djikstra as intersections. The costs to go from each intersection would be the street segment travel time and turn penalty. 
  * Why not A*: Djikstra passed all of the performance tests whereas, the time to calculate A*'s estimated values took too long. Our A* implementation is done through the Manhattan approach. This heuristic assumes that we can only take L's. Also we checked if an extra turn was needed from now until the end.
  * How our code is unique: Prof's initial code looked at if the current node's best time was greater than the wavefront's best time then current node would be updated. Our code changes this to catch some corner cases by looking at if the next node's best time was greater than its estimated time to reach there, then that path to the node would not be pushed on to the wave front. 
  * Considerations: To make our code faster, we returned the first path found. This implementation pass all the test cases and as a result we think it is good enough. However, if we wanted to be more thorough we could have let the algorithm run to find the most shortest path. Though that would have taken x2 the amount of time. Thus, we chose to return the first path. 

**Find Path with Walk: The second major function find path with walk to pick up are done by three team members together. All of three members contribute equally and a lot to make this function pass all of the test cases **
  * Implementation: 
  * First, find all walkable intersections. Perform Djikstra once to get all shortest paths to all walkable intersections. Determine if a new path is pushed onto the wave front if the best time to get to that node is less than the walking_time_limit. 
  * Second, get drive path. Perform Djikstra a second time, pushing all walkable intersections as the starting nodes. When the traceback occurs, it will reveal which walkable intersection was the starting node, thereby being the node that gives the shortest drive path.  
  * Third, get walk path. Perform a traceback from the starting node that gives the shortest drive path, all the way back to starting intersection.
====Tasks for each group member====


**Chaohe Li**: 

* Functions: *compute path travel time finished on Mar 19
             *bfs walk functions(for tracing back)

* Functions: *compute path walking time finished on Mar 19
             *Working on find path with walk to pick up from Mar 21-23. (keep trying but somewhat not working) Tried different method:First, find walkable intersections by using given walking speed and walking time limit to know how long the users can walk to. This can save compile time. And compare each possible intersections's driving time and save the best path when found one. 
* UI       : 
             *User should be able to enter the start point and the end point for path and a path will be highlighted finished on Mar 23
* UI       : 
             *Printing out detailed travel directions to the console Finished on Mar21 
             *Printing out required walking+driving time and driving time only on Mar22
             *Printing out detailed instructions for the navigation(for both drive and walk+drive only)
             *For example: This trip will approximately take 25 minutes.Please turn right in 150m.
             *Changing colours of the texting on terminal to make it more distinct
             *determine the directions of turning using algebraic calculations
* UI       : 
             *Give informative error messages if the user mistypes something (e.g. an invalid street or map name).   
             *Importing pngs for icons when users inputting starting and ending points for paths.
             *Drawing path between two intersections(similar method of drawing streets)
             *consider the case where the street segments have curve points and connect the curve points and street segments together. 

           
**Jackson Nie**:

* Functions:  *find path with walk to pick up, initial implementation passed few functionality tests on march 23, function was debugged and finished on Mar 24 with the help of Ryan.

*UI       : *Users must be able to enter commands that exercise your code to find a path between two intersections. Finished input mechanism on March 24 as well as error detecting and output mechanism. Finished highlight mechanism as well as improved on the input mechanism on March 26

*UI       : *Users must also be able to find paths between intersections by mouse clicking on intersections. Prototype finished by Ryan on March 22, added method to draw curve points on march 26 so that the path that was drawn is concise and represents the actual path.

*UI       :  *Your interface must have some method that allows users to specify partial names. Implemented find intersection id by partial intersection name function to allow users to type in partial intersection names, and the ui would print all possible matches. Finished March 24.

*UI.       :   Implemented basic highlight mechanism for all path drawing functions as well as concise input mechanism/ error detection for all path drawing functions. Finished March 26.

**Ryan Chang**:

* Functions: 
              *find path between intersections (description can be seen above) (Finished March 26th after multiple iterations)
              *find path with walk (description can be seen above) (Finished March 24th)

* UI       : 
              *Synchronize three different methods (walk and drive, drive path, and clicking on two points) so that only one would be displayed at time. (finished march 26)
              *Allow users to click on two points and draw the path between them, with icons representing the starting and ending points. Show messages to help them through the process. (Finished March 22)
              *Add a toggle button to remove paths from the screen. This is to let the user be able to click on intersections without drawing a path. (finished march 22)



**Internal deadline for functions implemention is Mar 23 (Monday)** Finished on time
**Internal deadline for UI implemention is Mar 25 (Wednesday)**. Finished on time
**Tuesday(Deadline) is for coding styles and final check of the program**
   * e.g make sure all of the warnings are gone 
   * e.g making variables names meaningful (global variables)



===== Milestone 1 =====
====== Week of January 27 ======

====January 24 2020====

Today, we had our first meeting with our TA and CI. Also,we are going to start milestone1 today. we try to divide 14 functions into 3 parts. Each of team member are responsible for four of them and the remaining two functions will be finished by all of us together. 


====January 25 2020====

Milestone 1 Plan

Chaohe Li
will write 5 m1.h functions
 1. find distance between two points
 2. find street segment length
 3. find street segment travel time
 4. find closet intersection 
 5. find feature area 


Jackson NIe
 will write 4 m1.h functions
 1. find street segments of intersection
 2. find street names of intersection
 3. are directly connected 
 4. find adjacent intersections


Ryan
 will write 4 m1.h functions
 1. find street segments of street
 2. find intersection of street
 3. find intersection of two streets 
 4. fund street ids from partial street name 

Together: load map close map find way length 

Our internal deadline for these functions to pass the function test is Jan31 
After the internal deadline, we will work together to try to pass all of the performance tests 

====January 29 2020====

We are able to pass 31 of 41 tests. We will need to do one last function "find way length" together and speed up the function 
of "Find Distance Time"

Our goal is to pass all of the tests before Sunday Feb 1st.
The deadline for Milestone1 is Feb 4th.

After finishing milestone1, our goal is to start thinking about Written Document 1. 

====January 30 2020====
Today, we are able to pass 39 of 41 cases. We still need to work on passing one function performance time
and there is one issue about loading the map which we will talk more with our TA during our tutorial tomorrow. 



======Week of February 3 2020======
====February 3 2020====
Debugged the code for load maps and find_intersection_of_two_streets. 

Passed all functionality and performance tests, and submitted the milestone 1
====February 6 2020====
Wrote proposal CI meeting. Set the internal deadline for Written Document 1 to be 7:00 P.M. 

February 15. Each team member should be done their individual parts. 

The remaining time is for the team members to iterate the document.
====February 7 2020====
Met with CI. She gave suggestions on how to improve rough Written Document 1 draft. She told us to go deeper on 

each of the points describing the functionalities of different maps. For example, when saying the graphics are 

smooth, we should always define what smooth means and what features make the graphics seem smooth. She also told

us to be more concise on our writing, and get into the topic right away instead of doing long lines of 

introductions.
======Week of February 10 2020======
====February 10 2020====
*The written document 0 marks came out, and we found that we failed to meet our goals for the term. All three 
members on the team did poorly on the document.

*There will definitely be a significant amount of communicating required over the week.

*The team feels lost on how to do written document 1, as nobody received a mark they are satisfied with.

*The team decided to divide the written document into three parts, and each individual would work on their own 
part.

*The team decided to have an extra meeting with the CI to discuss how to improve on written document 1.


====February 11 2020====
*The team agreed to use all available time to work on written document 1.

*Milestone 2 will be done over the reading week. 

*The team feels that the top priority is written document 1 this week not only because it has an earlier deadline, but also because the team members hope to put in a great effort to receive a good mark.

====February 13 2020====
*Due to overall performance of our groups on written document 0,Our CI will be giving us extra help time today at 4:30 pm. This is a good opportunity for us to discuss more about our writing weakness and hopefully we will be taking advantage of this and make improvements on Written document 1. 

After meeting with our CI. Our CI give us following advices for written document 1 

* For graphics, need examples and a lot of concrete resources. 

* Proposals and SAR are connected to each other 

* Pay attention to the word count, proposal is the part where should has the largest amount of words

* Some additional features does not necessary need to be implemented in milestone2.

* Scholars prove as details as possible 

* Responsiveness - Specific numbers are needed to back up 

* Compare three GIS and compare each other. 

* Try to implement Made To Sticks Principles

Kris Li finishes draft for Weather Maps.

Jackson Nie finishes draft for Google Maps.

Ryan Chang finishes draft for ESRI Power Tools for Commercial Real  Estate.
====February 14 2020====
* By Monday, we will have set up a coordinate system, with every object mapped to a real world measurement in meters.

* By Wednesday, Ryan will draw all the streets. Jackson will draw all the intersections. Chaohe will draw the features with equirectangular map projection. If possible, add street/intersection/feature names while drawing.

* On Thursday, the team will meet up, help each other out with the parts, and proceed to plan additional features.

====== Milestone 2 ======
Tasks for each group member


**Ryan Chang**

* Draw all of the features 
    * Internal Deadline: February 25th 
    * Finished: February 28
    * Add data structures to determine what types of figures should be drawn first 
        * (chosen that all polygon features are drawn first from biggest surface area to smallest, this may not be the most usable setting however, it provides an easy implementation that isn't very costly for loading time)
        * Non polygon features will be drawn next at any order
    * Future plans: Improve on what polygons to draw


* Determine zoom in percentage
    * Internal Deadline: February 23th 
    * Finished: February 23
    * Determine based on the screen's initial world rectangle total area.
    * Determine current world rectangle total area
    * Create zoom percentage by dividing the two values.

* Adjust features and names of feature to display based on percentage
    * Internal Deadline: February 26 require a lot of testing to figure out what improves the responsiveness 
    * Finished: February 28
    * Determined based on the figure's area or length compared to total area and length 
    * Determined the borders for names of features based on current zoom and give a limit to ensure it displays. Also display the name at the center of the way length or the centre of the rectangle of all the points 
    * In future: Want to match with when the feature is also shown


* Colour code everything
    * Internal Deadline: February 28 because it is a quick fix
    * Finished: February 28 
    * Currently drawing all beaches, greenspaces, as green
    * All buildings as grey
    * All rivers, ponds, bodies of water are blue
    * In future: Do research for finding a professional colour scheme

* Extra Feature: 
    * Create function to easily create rectangle based on several points (finished february 26th)
    * Reposition camera based on search results (finished february 26th)
    * Add Text that describes nearest intersection to mouse click (february 24th)


**Chaohe Li**

*initial set up of the whole project 
     * Converting LatLon to x y coordinates 
     * finished on Feb 21)
     * Writing the implementations for mouse click functions 
     * (finished on Feb 21)

* Draw all of the streets 
     * (Internal deadline is Feb24,finished on Feb23)

* Add finding intersections between two streets button 
    * Add button 
    * (Adding the button on Feb 20 to enable group members easy editing) 

* Fulfilling all of the street names
    * Draw the street names 
    * (finished on Feb23 but have trouble rotating the names, finish rotating the names on Feb 26)
    * Ensure that one way streets are highlighted 
    * (internal deadline is Feb25, finish it on Feb25).
    * Rotating the street names according to the angles they line between segments.
    * (on Feb 26 finished it using arc tan function)

* Draw names of points of interests
   * Draw all of the points of interests 
   * (finish on Feb25)

* Draw names of all of intersections
   * Draw all of the intersections to make them more visible
   * (finish on Feb21) 

* Highlighting major roads from minor roads
   * (finish it on Feb 27 before the final deadline)
   * Using speed limits to highlight all of the highways 
   * if speed limits is lower than 40km/h they are residual roads

* Finding One Way Roads and show their directions by using arrows 
   * (internal deadline is Feb24, finish it before the deadline and ensure the arrows lie correctly orientation)


* Extra Feature: 
    * Information enclosed: One way, Major or Minor, Street Name, Intersections etc...
    * Creating a Popup Dialog Box to make the UI interface more attractive 
    * (Trying to do it on Feb 28,but run out of time)
    * Add a button for displaying a city's subway stations and add icons into the map
    * (implement it on Feb 29)


**Jackson Nie**

*initial set up of the whole project 
   * Internal deadline Feb 18 but finished on Feb 21.
   * Converting LatLon to x y coordinates 
   * Drawing intersections of the map, creating a skeleton where we could draw additional streets and features
   * Understand the handout and do all required tasks on the handout as well as follow tutorial and lecture slides.

* Add finding intersections between two streets button and functionality
    * Internal deadline Feb 25 as streets will be drawn by Feb 24, but finished on Feb 24 as the streets were drawn prior to the streets deadline. 
    * Add button
    * Display Input Messages for streets
    * Ensure that they exist, using modified version partial street names function that cancels out the duplicates
    * Print Matches of desired street if the street exists
    * Require user input until two distinct streets are identified or if the user chooses to exit the search
    * Highlight matches of intersections and zoom to the highlighted intersection
    * Remove Highlights when you click away
    * Also provide user a way to exit the button without reclicking the button itself

* Load desired map without re-compiling
    * Internal deadline Feb 28 as we did not notice this feature until the TA meeting. Finished on Feb 28
    * Displayed all choosable maps and would load the desired map based on user input
    * If the map exists, load the map
    * If the map does not exist, require new user input
    * User may also choose to terminate the program
    * Minor error occured due to forgetting to clear 2 vectors during the submission panic.

* Extra Feature: Major Roads from Minor Roads
    * Internal deadline Feb 27, finished on Feb 27 with some bugs with team member ChaoHe Li. 
    * Look in OSMDatabase and check tags for different ways to differentiate between major and minor roads
    * Decided to differentiate the streets using the speed limit of streets.
    * Store major roads and minor roads in different vectors
    * Draw two types of roads in different colour and maybe different thickness

* Extra Feature: Find Features
    * Internal deadline Feb 28, finished on Feb 29 due to the lack of basic features
    * Functions similar to the find button
    * Create Find Features button, after user click and user input, display whether or not the feature exists
    * If the feature does not exist, print error message
    * If the feature does exist, zoom map to the feature with matching feature name
    * Also provide user a way to exit the button without reclicking the button itself

* Extra Feature: Find Point of interest
    * Internal deadline Feb 28, finished on Feb 29 due to the lack of basic features
    * Functions similar to the find button
    * Create Find Point Of Interest button, after user click and user input, display whether or not the point of interest exists
    * If the point of interest does not exist, print error message
    * If the point of interest does exist, zoom map to the desired point of interest
    * Also provide user a way to exit the button without reclicking the button itself
    * As many point of interests have the same name, this extra feature can only find one out of all of the point of interests that have identical names. Did not have enough time to modify the function, and for the function to be more specific and concise, further modification will be required.



**Possibilities for extra features:**

* Implement additional highlighting functions when a user clicks the mouse, such as
highlighting a street, building, park, etc.
    * Show extra information on UI on the side
* Upgrade the Find button so that it can auto-complete or suggest street names, or find
an intersection even if there are minor spelling mistakes in the street names.
* Implement additional Find button features that allow the user to find streets, points of
interest, buildings, etc. by name.
* Extract useful live data such as traffic accidents from a web site and display this data on
your map.
   * Add connection to lib curl.
   * Search for online API for several cities
   * Add button to activate to prevent slowing down the maps


======Take Away and Reflections from Milestone2======

After submitting milestone2, our group has summaries our strength and weaknesses. We finished implementing all of the basic features required for Milestone2.However,some extra features required more time to do than our expected. For milestone 3 and milestone4. We need to plan them as early as possible.Addition, we will set more internal deadlines to keep our work consistent through the whole period. 

Attending lectures and tutorials are important. Attendance will give our team a basic sense of what is going on,Also, it gives a guided-lines of starting the milestone. 

Divide works to group members more effectively. This time, at the beginning of the progress of milestone2. We did not have a clear subtasks for everyone which results in late start of the milestone2. For future milestones or other courses' assignments.We need to make sure each member knows what to expect and what to do.

Submit early(at least a draft one). There was a small issue raised when we tried to submit the assignment Half hour before the deadline. There was an ASCII code error when caused that we could not submit the assignment at all even though we passed all of the test cases.We posted on piazza and instructors was kinda enough to give us extended deadline to submit the assignment.It turns out that we did not comment out one line of code which tracks through the time and the code involved printing out a non-english letter. Additionally, due to the panic during submission, the team forgot to clear two new vectors that were implemented on the day of submission because the team was too focused on how to submit the project for over 30 minutes before the deadline, and did not recheck/retest the map itself. So next time, we need to make sure to try to submit early enough to prevent these issues from happening again.
====== Week of February 17 ======
Milestone2 work flow 
|              ^ February 17 ^ February 18 ^ February 19 ^ February 20 ^ February 21 ^ February 22
^ Chaohe Li    |  Start planning      | initial set up of the map(implement code from tutorial      | drawing all of the intersections  | adding find button for the basic feature   | drawing all of the streets  | drawing all of the points of interests| add names for the points of interests
^ Jackson Nie  |  Start planning      | initial set up of the map     | drawing all of the intersections  |Brainstormed how to load maps without re-compiling     |       |    |   |  |
^ Ryan Chang   |  Start planning      |  initial set up of the map       | drawing all of the features    |         |       |  |   |  | |


====== Week of February 24 ======
Milestone2 work flow 
|              ^ February 24 ^ February 25 ^February 26 ^February 27 ^February 28 ^ February 29 
^ Chaohe Li    | Add find button     | trying to make street names fitted in the middle of the street segment        | Highlighting the one way streets   |Working on adding more extra features |Add an user interface |Creating a popup dialog box     |    |   |
^ Jackson Nie  | Debugged the find button and made it work 90%, still shows duplicates         |         |     |Brainstormed / tried to add more extra features         |Looked through tags to see how to differentiate between major and minor streets, decided to use speed limit, completely debugged the find button, and implemented functionality of load other maps without recompiling.      |Implemented 2 extra features: find feature and find point of interest, deleted useless comments and iterated the project (not perfectly as the submission panic occured and we forgot to clear some vectors)    |  ||
^ Ryan Chang   |Add Text that describes nearest intersection to mouse click|Add highlights after finding intersection of 2 streets         | Re-position camera for different search results|Add way features to adjust how much is seen based on zoom in|   |Add colour coding for different features  |   |  | |



====== Milestone 3 ======
===Tasks for each group member===
**Chaohe Li**: 
* Functions: 
             *compute path travel time 
* Functions: 
             *compute path walking time
* UI       : 
             *User should be able to enter a walking speed and walking time limit as well as the start and end intersections 
* UI       : 
             *Must print out detailed travel directions to the console or in the graphics

           
**Jackson Nie**:
* Functions: 
              *find path with walk to pick up 
* UI       : 
              *Users must be able to enter commands that exercise your code to find a path betweentwo intersections
* UI       : 
              *Users must also be able to find paths between intersections by mouse clicking on intersections.


**Ryan Chang**:
* Functions: 
              *find path between intersections

* UI       : 
              *Must display the found path(s) in the user interface; for full marks this path shouldbe easy to understand and give a good sense of how to follow it.
* UI       : 
              *Must have some method (e.g. a help GUI button or notes in dialog boxes) so newusers can learn the interface.


**Whoever finish all of the assigned tasks can work on this one** 
           *Must give informative error messages if the user mistypes something (e.g. an invalidstreet or map name).


**Internal deadline for functions implemention is Mar 21 (Saturday)**
**Internal deadline for UI implemention is Mar 23 (Monday)**

====== Team Charter: ======


====What type of leadership do you want for your team?====
Democratic leadership.
All team members get to get involved in decision making and everyone's opinoin is taken into account and respected. Discuss the decision first,if there is consensus then go with the decision. If not, discuss pros and cons and take a vote. We prefer the team with no actual "leader" but everyone can play as a leader role as long as the other two group members agree with others together. 

====How will your team make decisions?====
1.Recognize the problem. 2.Gather information. 3.Develop Alternative Solutions.
Our team will make decisions based on everyone's ideas. We will need to have a group meeting before making any big decisions. This is to best avoid any unagreeable things. 

====How will you make yourselves accountable?====
Be involoved with each other. Communicating with each other freqeuntly. Be frank and honest with own situations.Do not hide or escape from team members' texts or calls. Be honest with each other. Always make comments on what other said or did. 

====How will you show respect?====Creating a 
Be a good listener. Respecting each other is really important for a team. Our team members should show respect to each other. Each team member is supposed to respect what other team members' ideas,coding,and thinkings to avoid any unnecessary conflicts between the team members.Be Kind to team members if any of team member has emergency issues. Be Thankful to the team memebers who give any helps.Have eye contacts with each other when speaking to each other. 
