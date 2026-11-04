# Lab 2 : Uninformed Search — BFS and DFS on a 2D Maze

# Exersice 1 : Compare BFS and DFS

We compare BFS and DFS based on their path lengths and maximum frontier sizes.

| Algorithm | Path Length | Maximum Frontier |
|-----------|-------------|------------------|
| BFS       | 8           | 3                |
| DFS       | 8           | 3                |

 
# Answer of the following questions 

1. Which algorithm found the shorter path?

   Neither. Both BFS and DFS found paths of equal length (8).

2. Which algorithm had the larger maximum frontier?

   Neither. Both had the same maximum frontier size (3).

3. Why did the two algorithms produce different paths on the same maze?

   Because BFS and DFS explore the maze differently. BFS explores level by level, while DFS follows one direction as far as possible before backtracking.

4. Does DFS always produce the shortest path? Why or why not?

   No. DFS may find a longer path first because it does not explore level by level.

5. Does BFS always produce the shortest path when every movement costs 1? Why?

   Yes. BFS explores level by level, so it finds the shortest path first when every movement has equal cost.

# Experiment 2 : Change the Neighbor Order

**DFS's exact path depends on the order in which neighbors are tried. Change directions and re-run DFS:**

# Before Changing Neighbor Order:
**Original directions:**

(-1, 0) → up

(1, 0) → down

(0, -1) → left

(0, 1) → right


**Output:**

DFS path: [(0, 0), (0, 1), (0, 2), (0, 3), (0, 4), (1, 4), (2, 4), (3, 4), (4, 4)]

DFS path length: 8

DFS maximum frontier: 3

# After Changing Neighbor Order

New directions:

(0, 1) → right

(1, 0) → down

(0, -1) → left

(-1, 0) → up


**Output:**

DFS path (new order): [(0, 0), (1, 0), (2, 0), (2, 1), (2, 2), (3, 2), (3, 3), (3, 4), (4, 4)]

DFS path length: 8

DFS maximum frontier: 3

# Did the DFS path change? Did BFS's path depend on this ordering the same way? Why or why not?

The DFS path changed because DFS follows neighbors according to their given order.

BFS also uses the neighbor order when choosing between multiple paths of equal length. However, BFS still finds a shortest path when every movement costs 1. The path length remains shortest, even if the exact path changes.


# Experiment 3 : Change start and goal

start = (0, 0)

goal = (2, 2)

BFS path: [(0, 0), (1, 0), (2, 0), (2, 1), (2, 2)]

BFS path length: 4

BFS maximum frontier: 3


DFS path: [(0, 0), (0, 1), (0, 2), (0, 3), (0, 4), (1, 4), (2, 4), (3, 4), (3, 3), (3, 2), (2, 2)]

DFS path length: 10

DFS maximum frontier: 3

Run the Experiment 3 time

### Run the experiment with three different start and goal pairs.

| **Start** | **Goal** | **BFS Length** | **BFS Max Frontier** | **DFS Length** | **DFS Max Frontier** |
|-----------|----------|----------------|----------------------|----------------|----------------------|
| (0, 0)    | (2, 2)   | 4              | 3                    | 10             | 3                    |
| (0, 0)    | (3, 4)   | 7              | 3                    | 7              | 2                    |
| (2, 0)    | (4, 4)   | 6              | 3                    | 6              | 4                    |


6. Does BFS's path length ever change if you re-run it with the same start/goal? Does DFS's?

  BFS always finds the shortest path, so its path length remains the same. DFS may find a different path if the neighbor order changes, so its path length can also change.

7. As the distance between start and goal grows, what happens to the maximum frontier size for each algorithm?

   The maximum frontier may increase as the distance grows because the algorithms may need to explore more cells. However, it does not always increase.

8. Can you find a (start, goal) pair where BFS and DFS return the same path? What does that tell you about the maze structure between those two points?

   Yes. Both algorithms can return the same path when there is a direct route and their exploration order follows that route. It means there may be only one suitable path between those points.

9. What happens if goal is unreachable from start (e.g. sealed off by walls)? Try it — what do bfs() and dfs() return?

   Both algorithms explore all reachable cells. If the goal cannot be reached, both return None for the path and return the maximum frontier size.


