Download Link: https://assignmentchef.com/product/solved-ve492-project-1-search-2
<br>
In this project, your Pacman agent will find paths through his maze world, both to reach a particular location and to collect food efficiently. You will build general search algorithms and apply them to Pacman scenarios.

The code for this project consists of several Python files, some of which you will need to read and understand in order to complete the assignment, and some of which you can ignore. You can download all the code and supporting files from <a href="https://umjicanvas.com/files/209164/download?download_frd=1">P1.zip</a> in the folder Projects on Canvas.

<table width="0">

 <tbody>

  <tr>

   <td colspan="2" width="517"><strong>Files you’ll edit:</strong></td>

  </tr>

  <tr>

   <td width="164">search.py</td>

   <td width="353">Where all of your search algorithms will reside.</td>

  </tr>

  <tr>

   <td width="164">searchAgents.py</td>

   <td width="353">Where all of your search-based agents will reside.</td>

  </tr>

  <tr>

   <td colspan="2" width="517"><strong>Files you might want to look at:</strong></td>

  </tr>

  <tr>

   <td width="164">pacman.py</td>

   <td width="353">The main file that runs Pacman games. This file describes a Pacman GameState type, which you use in this project.</td>

  </tr>

  <tr>

   <td width="164">game.py</td>

   <td width="353">The logic behind how the Pacman world works. This file describes several supporting types like AgentState, Agent, Direction, and Grid.</td>

  </tr>

  <tr>

   <td width="164">util.py</td>

   <td width="353">Useful data structures for implementing search algorithms.</td>

  </tr>

  <tr>

   <td colspan="2" width="517"><strong>Supporting files you can ignore:</strong></td>

  </tr>

  <tr>

   <td width="164">graphicsDisplay.py</td>

   <td width="353">Graphics for Pacman</td>

  </tr>

  <tr>

   <td width="164">graphicsUtils.py</td>

   <td width="353">Support for Pacman graphics</td>

  </tr>

  <tr>

   <td width="164">textDisplay.py</td>

   <td width="353">ASCII graphics for Pacman</td>

  </tr>

  <tr>

   <td width="164">ghostAgents.py</td>

   <td width="353">Agents to control ghosts</td>

  </tr>

  <tr>

   <td width="164">keyboardAgents.py</td>

   <td width="353">Keyboard interfaces to control Pacman</td>

  </tr>

  <tr>

   <td width="164">layout.py</td>

   <td width="353">Code for reading layout files and storing their contents</td>

  </tr>

 </tbody>

</table>




<h1>Welcome to Pacman</h1>

After downloading the code <a href="https://umjicanvas.com/files/209164/download?download_frd=1">P1.zip</a> , unzipping it, and changing to the directory, you should be able to play a game of Pacman by typing the following at the command line: python pacman.py

Pacman lives in a shiny blue world of twisting corridors and tasty round treats. Navigating this world efficiently will be Pacman’s first step in mastering his domain.

The simplest agent in searchAgents.py is called the GoWestAgent, which always goes West (a trivial reflex agent). This agent can occasionally win:

python pacman.py –layout testMaze –pacman GoWestAgent But, things get ugly for this agent when turning is required: python pacman.py –layout tinyMaze –pacman GoWestAgent

If Pacman gets stuck, you can exit the game by typing <strong>CTRL-c </strong>into your terminal.

Soon, your agent will solve not only tinyMaze, but any maze you want. Note that pacman.py supports a number of options that can each be expressed in a long way (e.g., –layout) or a short way(e.g., -l). You can see the list of all options and their default values via:

python pacman.py -h

Also, all of the commands that appear in this project also appear in commands.txt, for easy copying and pasting. In UNIX/Mac OS X, you can even run all these commands in order with bash commands.txt.

<h1>Question 1: Finding a Fixed Food Dot using Depth First Search</h1>

In searchAgents.py, you’ll find a fully implemented SearchAgent, which plans out a path through Pacman’s world and then executes that path stepby-step. The search algorithms for formulating a plan are not implemented – that’s your job.

First, test that the SearchAgent is working correctly by running:

python pacman.py -l tinyMaze -p SearchAgent -a fn=tinyMazeSearch

The command above tells the SearchAgent to use tinyMazeSearch as its search algorithm, which is implemented in search.py. Pacman should navigate the maze successfully.

Now it’s time to write full-fledged generic search functions to help Pacman plan routes! Pseudocode for the search algorithms you’ll write can be found in the lecture slides. Remember that a search node must contain not only a state but also the information necessary to reconstruct the path (plan) which gets to that state.

<em>Important note: </em>All of your search functions need to return a list of actions that will lead the agent from the start to the goal. These actions all have to be legal moves (valid directions, no moving through walls).

<em>Important note: </em>Make sure to <strong>use </strong>the Stack, Queue and PriorityQueue data structures provided to you in util.py! These data structure implementations have particular properties which are required for compatibility with the online judge.

<em>Hint: </em>Each algorithm is very similar. Algorithms for DFS, BFS, UCS, and A* differ only in the details of how the fringe is managed. So, concentrate on getting DFS right and the rest should be relatively straightforward. Indeed, one possible implementation requires only a single generic search method which is configured with an algorithm-specific queuing strategy. (Your implementation need <em>not </em>be of this form to receive full credit).

Implement the depth-first search (DFS) algorithm in the depthFirstSearch function in search.py. To make your algorithm <em>complete</em>, write the graph search version of DFS, which avoids expanding any already visited states. Your code should quickly find a solution for:

python pacman.py -l tinyMaze -p SearchAgent python pacman.py -l mediumMaze -p SearchAgent python pacman.py -l bigMaze -z .5 -p SearchAgent

The Pacman board will show an overlay of the states explored, and the order in which they were explored (brighter red means earlier exploration). Is the exploration order what you would have expected? Does Pacman actually go to all the explored squares on his way to the goal?

<em>Hint: </em>If you use a Stack as your data structure, the solution found by your DFS algorithm for mediumMaze should have a length of 130 (provided you push successors onto the fringe in the order provided by getSuccessors; you might get 246 if you push them in the reverse order). Is this a least cost solution? If not, think about what depth-first search is doing wrong.

<h1>Question 2: Breadth First Search</h1>

Implement the breadth-first search (BFS) algorithm in the breadthFirstSearch function in search.py. Again, write a graph search algorithm that avoids expanding any already visited states. Test your code the same way you did for depth-first search.

python pacman.py -l mediumMaze -p SearchAgent -a fn=bfs python pacman.py -l bigMaze -p SearchAgent -a fn=bfs -z .5

Does BFS find a least cost solution? If not, check your implementation.

<em>Hint: </em>If Pacman moves too slowly for you, try the option –frameTime 0. <em>Note: </em>If you’ve written your search code generically, your code should work equally well for the eight-puzzle search problem without any changes.

python eightpuzzle.py

<h1>Question 3: Varying the Cost Function</h1>

While BFS will find a fewest-actions path to the goal, we might want to find paths that are “best” in other senses. Consider mediumDottedMaze and mediumScaryMaze.

By changing the cost function, we can encourage Pacman to find different paths. For example, we can charge more for dangerous steps in ghost-ridden areas or less for steps in food-rich areas, and a rational Pacman agent should adjust its behavior in response.

Implement the uniform-cost graph search algorithm in the uniformCostSearch function in search.py. We encourage you to look through util.py for some data structures that may be useful in your implementation. You should now observe successful behavior in all three of the following layouts, where the agents below are all UCS agents that differ only in the cost function they use (the agents and cost functions are written for you):

python pacman.py -l mediumMaze -p SearchAgent -a fn=ucs python pacman.py -l mediumDottedMaze -p StayEastSearchAgent python pacman.py -l mediumScaryMaze -p StayWestSearchAgent

<em>Note: </em>You should get very low and very high path costs for the StayEastSearchAgent and StayWestSearchAgent respectively, due to their exponential cost functions (see searchAgents.py for details).

<h1>Question 4: A* search</h1>

Implement A* graph search in the empty function aStarSearch in search.py. A* takes a heuristic function as an argument. Heuristics take two arguments: a state in the search problem (the main argument), and the problem itself (for reference information). The nullHeuristic heuristic function in search.py is a trivial example.

You can test your A* implementation on the original problem of finding a path through a maze to a fixed position using the Manhattan distance heuristic (implemented already as manhattanHeuristic in searchAgents.py).

python pacman.py -l bigMaze -z .5 -p SearchAgent -a fn=astar,heuristic=manhattanHeuristic

You should see that A* finds the optimal solution slightly faster than uniform cost search (about 549 vs. 620 search nodes expanded in our implementation, but ties in priority may make your numbers differ slightly). What happens on openMaze for the various search strategies?

<h1>Question 5: Finding All the Corners</h1>

The real power of A* will only be apparent with a more challenging search problem. Now, it’s time to formulate a new problem and design a heuristic for it.

In <em>corner mazes</em>, there are four dots, one in each corner. Our new search problem is to find the shortest path through the maze that touches all four corners (whether the maze actually has food there or not). Note that for some mazes like tinyCorners, the shortest path does not always go to the closest food first! <em>Hint: </em>the shortest path through tinyCorners takes 28 steps.

<em>Note: Make sure to complete Question 2 before working on Question 5, because Question 5 builds upon your answer for Question 2.</em>

Implement the CornersProblem search problem in searchAgents.py. You will need to choose a state representation that encodes all the information necessary to detect whether all four corners have been reached. Now, your search agent should solve:

python pacman.py -l tinyCorners -p SearchAgent

-a fn=bfs,prob=CornersProblem

python pacman.py -l mediumCorners -p SearchAgent -a fn=bfs,prob=CornersProblem

To receive full credit, you need to define an abstract state representation that <em>does not </em>encode irrelevant information (like the position of ghosts, where extra food is, etc.). In particular, do not use a Pacman GameState as a search state. Your code will be very, very slow if you do (and also wrong). <em>Hint</em>: The only parts of the game state you need to reference in your implementation are the starting Pacman position and the location of the four corners.

Our implementation of breadthFirstSearch expands just under 2000 search nodes on mediumCorners. However, heuristics (used with A* search) can reduce the amount of searching required.

<h1>Question 6: Corners Problem: Heuristic</h1>

<em>Note: Make sure to complete Question 4 before working on Question 6, because Question 6 builds upon your answer for Question 4.</em>

Implement a non-trivial, consistent heuristic for the CornersProblem in cornersHeuristic.

python pacman.py -l mediumCorners -p AStarCornersAgent -z 0.5

<em>Note: </em>AStarCornersAgent is a shortcut for

-p SearchAgent -a

fn=aStarSearch,prob=CornersProblem,heuristic=cornersHeuristic

<em>Admissibility vs. Consistency: </em>Remember, heuristics are just functions that take search states and return numbers that estimate the cost to a nearest goal. More effective heuristics will return values closer to the actual goal costs. To be <em>admissible</em>, the heuristic values must be lower bounds on the actual shortest path cost to the nearest goal (and non-negative). To be <em>consistent</em>, it must additionally hold that if an action has cost c, then taking that action can only cause a drop in heuristic of at most c.

Remember that admissibility isn’t enough to guarantee correctness in graph search – you need the stronger condition of consistency. However, admissible heuristics are usually also consistent, especially if they are derived from problem relaxations. Therefore it is usually easiest to start out by brainstorming admissible heuristics. Once you have an admissible heuristic that works well, you can check whether it is indeed consistent, too. The only way to guarantee consistency is with a proof. However, inconsistency can often be detected by verifying that for each node you expand, its successor nodes are equal or higher in f-value. Moreover, if UCS and A* ever return paths of different lengths, your heuristic is inconsistent. This stuff is tricky!

<em>Non-Trivial Heuristics: </em>The trivial heuristics are the ones that return zero everywhere (UCS) and the heuristic which computes the true completion cost. The former won’t save you any time, while the latter will timeout the online judge. You want a heuristic which reduces total compute time, though for this assignment the online judge will only check node counts (aside from enforcing a reasonable time limit).

<em>Grading: </em>Your heuristic must be a non-trivial non-negative consistent heuristic to receive any points. Make sure that your heuristic returns 0 at every goal state and never returns a negative value. Depending on how few nodes your heuristic expands, you’ll be graded:

<em>Remember: </em>If your heuristic is inconsistent, you will receive <em>no </em>credit, so be careful!

<table width="0">

 <tbody>

  <tr>

   <td width="232"><strong>Number of nodes expanded</strong></td>

   <td width="65"><strong>Grade</strong></td>

  </tr>

  <tr>

   <td width="232">more than 2000</td>

   <td width="65">0/3</td>

  </tr>

  <tr>

   <td width="232">at most 2000</td>

   <td width="65">1/3</td>

  </tr>

  <tr>

   <td width="232">at most 1600</td>

   <td width="65">2/3</td>

  </tr>

  <tr>

   <td width="232">at most 1200</td>

   <td width="65">3/3</td>

  </tr>

 </tbody>

</table>

<h1>Question 7: Eating All The Dots</h1>

Now we’ll solve a hard search problem: eating all the Pacman food in as few steps as possible. For this, we’ll need a new search problem definition which formalizes the food-clearing problem: FoodSearchProblem in searchAgents.py (implemented for you). A solution is defined to be a path that collects all of the food in the Pacman world. For the present project, solutions do not take into account any ghosts or power pellets; solutions only depend on the placement of walls, regular food and Pacman. (Of course ghosts can ruin the execution of a solution! We’ll get to that in the next project.) If you have written your general search methods correctly, A* with a null heuristic (equivalent to uniform-cost search) should quickly find an optimal solution to testSearch with no code change on your part (total cost of 7).

python pacman.py -l testSearch -p AStarFoodSearchAgent

<em>Note: </em>AStarFoodSearchAgent is a shortcut for

-p SearchAgent -a fn=astar,prob=FoodSearchProblem,heuristic=foodHeuristic

You should find that UCS starts to slow down even for the seemingly simple tinySearch. As a reference, our implementation takes 2.5 seconds to find a path of length 27 after expanding 5057 search nodes.

<em>Note: Make sure to complete Question 4 before working on Question 7, because Question 7 builds upon your answer for Question 4.</em>

Fill in foodHeuristic in searchAgents.py with a <em>consistent </em>heuristic for the FoodSearchProblem. Try your agent on the trickySearch board: python pacman.py -l trickySearch -p AStarFoodSearchAgent

Our UCS agent finds the optimal solution in about 13 seconds, exploring over 16,000 nodes.

Any non-trivial non-negative consistent heuristic will receive 1 point. Make sure that your heuristic returns 0 at every goal state and never returns a

<table width="0">

 <tbody>

  <tr>

   <td width="232"><strong>Number of nodes expanded</strong></td>

   <td width="233"><strong>Grade</strong></td>

  </tr>

  <tr>

   <td width="232">more than 15000</td>

   <td width="233">1/4</td>

  </tr>

  <tr>

   <td width="232">at most 15000</td>

   <td width="233">2/4</td>

  </tr>

  <tr>

   <td width="232">at most 12000</td>

   <td width="233">3/4</td>

  </tr>

  <tr>

   <td width="232">at most 9000</td>

   <td width="233">4/4(full credit; medium)</td>

  </tr>

  <tr>

   <td width="232">at most 7000</td>

   <td width="233">5/4(optional extra credit; hard)</td>

  </tr>

 </tbody>

</table>

negative value. Depending on how few nodes your heuristic expands, you’ll get additional points:

<em>Remember:</em>If your heuristic is inconsistent, you will receive no credit, so be careful! If your number of nodes expanded is less than 7000, you can get 5% of bonus point in project 1.

Hint: You can create your own heuristic function with the search method you have implemented in the previous problems.

<h1>Question 8: Suboptimal Search</h1>

Sometimes, even with A* and a good heuristic, finding the optimal path through all the dots is hard. In these cases, we’d still like to find a reasonably good path, quickly. In this section, you’ll write an agent that always greedily eats the closest dot. ClosestDotSearchAgent is implemented for you in searchAgents.py, but it’s missing a key function that finds a path to the closest dot.

Implement the function findPathToClosestDot in searchAgents.py. Our agent solves this maze (sub-optimally!) in under a second with a path cost of 350:

python pacman.py -l bigSearch -p ClosestDotSearchAgent -z .5

<em>Hint:</em>The quickest way to complete findPathToClosestDot is to fill in the AnyFoodSearchProblem, which is missing its goal test. Then, solve that problem with an appropriate search function. The solution should be very short!

Your ClosestDotSearchAgent won’t always find the shortest possible path through the maze. Make sure you understand why and try to come up with a small example where repeatedly going to the closest dot does not result in finding the shortest path for eating all the dots.