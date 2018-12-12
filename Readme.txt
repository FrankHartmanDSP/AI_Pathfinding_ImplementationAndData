README CSCI 4511W Final Project Implementation and Data Collection

Franklin Hartman and Ethan Marshall

Github Repo Link: https://github.com/marsh806/AI_Implementation_Actual.git



****Included Data:****



	/data/figures/

In this folder, we have included all the figures we have created for this project. Generally speaking, each subfolder in this folder represents a specific pathfinding algorithm and contains three PNG files. Each of these three PNG files represents the three environments we have tested the pathfinding algorithm on. In each environment, the start point is on the left (represented by a small white dot) while the target point is on the right (represented by a larger white dot). Obstacles are represented by red squares, “walkable” terrain is represented by a green plane, and the path chosen by the algorithm is drawn with a black line.

	/data/figures/dijkstra, /data/figures/astar, /data/figures/smoothastar

The three pathfinding algorithms which are represented in each subfolder are Dijkstra’s algorithm, A* Search, and a smooth path variant of A* Search dubbed “Smoothed A* Search”.

	/data/figures/smoothastar/turnDist2, /data/figures/smoothastar/turnDist5

Within the smoothed astar folder, there are two subfolders. Each of these represents the algorithm’s performance in the 3 environments with a different turn distance value. This turn distance value determines the size of the curve in path turns.

	/data/figures/environments

This subfolder contains the blank environments before a pathfinding algorithm has been ran.

	/data/tables/data.xlsx

This Microsoft Excel file contains data collected concerning run times and memory usage. The three different sections signify the different environments tested (each environment corresponds to an increase in complexity). Nodes created shows the memory usage, path runtime shows the time the algorithm took to find the path, and smoothing runtime shows how long it took to make calculations necessary for smoothing the found path. Since Dijkstra’s and regular A* don’t include any smoothing component, this field is listed as non-applicable in those cases. The 2 and 5 variations on A* Smooth indicate the turn radius used for the smoothing component. Furthermore, the results of a survey conducted are available at the bottom of the file. The survey was given by showing each participant how the three algorithms chose paths in an environment and asking them to pick which seemed the most realistic. This was carried out for each of the three environments.



****Included code:****



PLEASE NOTE: The following code has been modified from GitHub user SebLague rom GitHub and all modifications made are noted. If desired, the source code is visible at this link:
https://github.com/SebLague/Pathfinding


	/A Star and Djikstra/
	/Smoothed A Star/

These parent folders contain unity projects with all our custom environments. The A Star and Djikstra parent folder contains both the A Star and Dijkstra pathfinding algorithms, the latter of which has been added in by us. In order to switch from A* to Dijkstra, one must tick this boolean value on the A* asset within the scene. The second parent folder contains only the Smoothed A* variant of A*, which has been modified to not include path weighting and to include path tracing.




****The following subfolders are common to both the “A Star and Djikstra” and “Smoothed A Star” parent folders****

	/v15

This is a standard unity folder contains necessary files for Unity to communicate with its server. Nothing was changed.

	/Assets

This folder holds the materials, models, and scripts used in the project. Additionally, the different Unity environments that are being tested are stored here.

	/Assets/Env1.unity , /Assets/Env2.unity , /Assets/Env3.unity

These files are the environments being tested. Please note that each environment was custom made by us for the purpose of testing in this project. Each environment consists of a plane, obstacles, a seeker, and a target. The plane represents the searchable space of the algorithm. The seeker and target represent the initial location and goal location respectively. The obstacles are the representation of the constraints.

	/Assets/Materials

This folder holds all of the material files used in the project, which essentially are colors / color schemes applied to various game objects, making the objects appear in that color / color scheme (please note that although the path material only appears in the smoothed a star Unity project, it was ultimately not utilized in our implementation).

	/Assets/Scripts

This folder contains all of the scripts used in the unity file, specifically those implementing the algorithms that are being tested.

	/Library/

This folder contains all Unity-supplied library files necessary to run this scene.

	/obj/

This folder is used to store files generated during build.

	/Packages/manifest.json

Contains all project dependencies.

	/ProjectSettings/

This folder stores all project settings from the unity scene (anything altered by clicking edit>project settings)




****The following subfolders pertain to ONLY the “A Star and Djikstra” parent folder****

	/A Star and Djikstra.sln

This is a solution file for IDEs.

	/Assembly-CSharp.csproj

Visual Studio project file generated for scripts.

	/builds/

Contains a test build used during data gathering.

	/Assets/Scripts/Node.cs

This is the class declaration and implementation of a Node used in the algorithm.

	/Assets/Scripts/Grid.cs

This is the class declaration and implementation of a Grid used in the algorithm as the searchable space.

	/Assets/Scripts/Heap.cs

This is the class declaration of a heap that is used to optimize performance. It is the same across all three algorithms and therefore is a constant to performance.

	/Assets/Scripts/Pathfinding.cs

This is the class declaration of the Pathfinding class, which contains the logic regarding implementing Dijkstra’s and A*. The changes made include the implementation of Dijkstra’s algorithm. This is introduced via a boolean variable that indicates whether or not the code is operating as Dijkstra or A*. This operates by setting the heuristic value to zero when Dijkstra being used, and leaving it as is when A* is being used.




****The following subfolders pertain to ONLY the “Smoothed A Star” parent folder****

	/Smoothed A Star.sln

This is a solution file for IDEs.

	/Assembly-CSharp.csproj

Visual Studio project file generated for scripts.

	/Assets/Scripts/Node.cs

This is the class declaration and implementation of a Node used in the algorithm.

	/Assets/Scripts/Grid.cs

This is the class declaration and implementation of a Grid used in the algorithm as the searchable space.

	/Assets/Scripts/Heap.cs

This is the class declaration of a heap that is used to optimize performance. It is the same across all three algorithms and therefore is a constant to performance.

	/Assets/Scripts/Path.cs

This is the class declaration of a path, which (when combined with the Line class) defines certain features about paths pertinent to smoothing paths. This includes the definition of turn boundaries for the entire path, which is the determining factor for when a Unit will begin to turn towards the next waypoint (both Units and waypoints will be explained later). 

	/Assets/Scripts/Pathfinding.cs

This is the class declaration of the Pathfinding class, which contains the logic regarding implementing A* to find the path. This is largely similar to the implementation in “A Star and Djikstra”, but modified to work with Units. Additionally, this implementation also simplifies the path after it has been found by A*. This amounts to a removal of nodes which are in a straight line, leaving only the turning points (where the angular direction of the current path changes). These turning points are referred to as “way points”, and are represented using vectors. These vectors represent the direction and magnitude the path is pointing in from the current point. An array of these vectors represents a larger path.
Originally, weights were included to assign to certain “terrains” within the environment. However, this aspect of the code was removed to achieve a constant weight among all paths. The weighting added different movement penalties for the agent traversing the environment (in “game” terms, this would be the difference between a road and a bog), but the scope of our project did not include the study of this.

	/Assets/Scripts/Line.cs

This is the class declaration of the line class, which was used to store information about lines pertinent to the creation of smooth paths. This includes the ability to check whether a Unit at a current point in a path has crossed the turn boundary, meaning it should begin turning to the next waypoint.

	/Assets/Scripts/Unit.cs

This is the class declaration for the Unit class, which is used to represent the agent traversing across the path. Additionally, this class also contains the implementation for the path smoothing of interest in this Unity project. Using the waypoints determined from Pathfinding.cs, the Unit in question is able to follow the entire path.

	/Assets/Scripts/PathRequestManager.cs

This is the class declaration for the PathRequestManager class, which is used to handle a queue of path requests, allowing for multiple Units to find paths concurrently.





REFERENCES
https://github.com/SebLague/Pathfinding Online, Normal A* and Smoothed A* implementation in Unity
