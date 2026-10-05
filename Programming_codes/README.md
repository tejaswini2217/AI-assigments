## Dijkstra Shortest Path

### Project Overview

This part of the project finds the **shortest path between two Indian cities** using **Dijkstra's Algorithm**.

The city and distance information is taken from the `indian-cities-dataset.csv` file.

### Technologies Used

* Python
* Pandas
* Dijkstra's Algorithm
* `heapq`

### How It Works

1. Load the Indian cities dataset using Pandas.
2. Create a graph using the Origin, Destination, and Distance columns.
3. Connect cities in both directions.
4. Take the start city and goal city from the user.
5. Apply Dijkstra's Algorithm to find the shortest path.
6. Display the path and total distance.

### Graph

Each city is treated as a **node** and the distance between two cities is treated as the **edge weight**.

### Dijkstra's Algorithm

Dijkstra's Algorithm finds the shortest path from a starting city to a destination city based on the minimum total distance.

The program uses `heapq` to efficiently select the city with the smallest distance.

### Input

The user enters:

* Start city
* Goal city

Example:

```text
Enter start city: Hyderabad
Enter goal city: Bangalore
```

### Output

The program displays:

```text
Shortest Path:
Hyderabad -> ... -> Bangalore

Total Distance: ... km
```

### City Name Correction

The program also handles the common spelling:

`Visakhapatnam` → `Vishakhapatnam`

### Conclusion

This project demonstrates how **Dijkstra's Algorithm** can be used to find the shortest route between cities based on distance.


# UGV Navigation

## Project Overview

This project finds the shortest path for an **Unmanned Ground Vehicle (UGV)** using the **A* algorithm**.

The program creates a **70 × 70 grid** with random obstacles. The user selects:

* Obstacle density
* Start position
* Goal position

The A* algorithm finds a path from the start to the goal.

## Technologies Used

* Python
* A* Algorithm
* `heapq`
* `random`

## How It Works

1. Create a 70 × 70 grid.
2. Generate random obstacles.
3. Select the start and goal positions.
4. Use the A* algorithm to find a path.
5. Display the path in the grid.

## Obstacle Density

* **Low** → 10% obstacles
* **Medium** → 20% obstacles
* **High** → 30% obstacles

## A* Algorithm

A* uses:

**f(n) = g(n) + h(n)**

* `g(n)` = cost from start
* `h(n)` = estimated distance to goal
* `f(n)` = total cost

The project uses **Manhattan distance**.

## Movement

The UGV can move:

* Up
* Down
* Left
* Right

Diagonal movement is not allowed.

## Grid Symbols

* `S` → Start
* `G` → Goal
* `*` → Path
* `#` → Obstacle
* `.` → Empty space

## Output

If a path is found, the program displays:

* Start position
* Goal position
* Path length
* Nodes explored
* UGV path

If no path is possible, it displays **"No path exists!"**

## Conclusion

This project demonstrates how the **A* pathfinding algorithm** can be used for UGV navigation in a grid with obstacles.
3. Grid_problem

What does this code do?

This program extends the first UGV navigation program by introducing
dynamic obstacles.

The UGV initially finds a path using A*. While the UGV is following the
path, new obstacles can appear randomly.

If a newly created obstacle blocks the UGV's planned path, the program
performs replanning.

Working

Create a 70 × 70 grid.

Generate the initial random obstacles.

Get the start and goal positions from the user.

Use A* to find a path.

Start moving the UGV along the path.

Randomly introduce new obstacles while the UGV is moving.

Check whether the next position is blocked.

If the path is blocked, stop the current path.

Run A* again from the UGV's current position.

Continue until the UGV reaches the goal or no path is available.

Dynamic Obstacle

During movement, the program has a 5% probability of generating a new
obstacle at a random position.

The program makes sure that the newly generated obstacle does not
replace:

The current UGV position

The goal position

Replanning

When the next position becomes blocked:

Path blocked
     ↓
Re-planning
     ↓
Run A* again
     ↓
Continue toward goal

The program keeps track of:

final_path -- positions followed by the UGV

total_nodes_explored -- total nodes explored across A* searches

replanning_count -- number of replanning operations
Grid                       70 × 70             70 × 70
Algorithm                  A*                 A*
Random initial obstacles   Yes                 Yes
Dynamic obstacles          No                  Yes
Replanning                 No                  Yes
Four-direction movement    Yes                 Yes
Manhattan heuristic        Yes                 Yes
Path tracking              Yes                 Yes
Nodes explored             Yes                 Yes
Replanning count           No                  Yes
**conclusion**
## Conclusion

The Grid_problem successfully demonstrates UGV navigation in a dynamic environment. The UGV can detect obstacles and replan its path using the A* algorithm to reach the goal.

