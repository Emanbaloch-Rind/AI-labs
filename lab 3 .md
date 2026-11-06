# Lab 3: Informed Search — A* Search for the 8-Puzzle

# Exercise 1: Implement Misplaced Tiles Heuristic

```python
def misplaced_tiles(state):
    count = 0

    for i in range(9):
        if state[i] != 0 and state[i] != GOAL_STATE[i]:
            count += 1

    return count
```
```python
GOAL_STATE = (1, 2, 3, 4, 5, 6, 7, 8, 0)
```

```python
def misplaced_tiles(state):
    count = 0

    for i in range(9):
        if state[i] != 0 and state[i] != GOAL_STATE[i]:
            count += 1

    return count
```
```python
test_state = (1, 2, 3, 4, 5, 6, 7, 0, 8)
result = misplaced_tiles(test_state)

print("Misplaced Tiles:", result)
```
Misplaced Tiles: 1

# Exercise 2: Implement Manhattan Distance Heuristic
```python
def manhattan_distance(state):
    distance = 0

    for i in range(9):
        tile = state[i]

        if tile != 0:
            current_row, current_col = divmod(i, 3)
            goal_row, goal_col = divmod(tile - 1, 3)

            distance += abs(current_row - goal_row) + abs(current_col - goal_col)

    return distance
```
```python
test_state = (1, 2, 3, 4, 5, 6, 7, 0, 8)

result = manhattan_distance(test_state)

print("Manhattan Distance:", result)
```
Manhattan Distance: 1

# Exercise 3: Implement A* Search Algorithm

```python

import heapq
import itertools
def a_star_search(start_state, heuristic_fn):

    counter = itertools.count()
    frontier = []

    heapq.heappush(frontier, (
        heuristic_fn(start_state),
        next(counter),
        0,
        start_state,
        []
    ))

    best_g = {start_state: 0}
    nodes_expanded = 0
 ```
```python
    while frontier:
        f, _, g, state, path = heapq.heappop(frontier)

        nodes_expanded += 1

        if state == GOAL_STATE:
            return {
                "path": path,
                "cost": g,
                "nodes_expanded": nodes_expanded
            }
```
```python
        if g > best_g[state]:
            continue
```
```python
        for neighbor_state, action in get_neighbors(state):
            new_g = g + 1

            if neighbor_state not in best_g or new_g < best_g[neighbor_state]:
                best_g[neighbor_state] = new_g
                new_f = new_g + heuristic_fn(neighbor_state)

                heapq.heappush(frontier, (
                    new_f,
                    next(counter),
                    new_g,
                    neighbor_state,
                    path + [action]
                ))
```

```pyhon
    return {
        "path": None,
        "cost": None,
        "nodes_expanded": nodes_expanded
    }
```
```python

easy_state = (1, 2, 3, 4, 5, 6, 7, 0, 8)

result = a_star_search(easy_state, manhattan_distance)

print(result)
```
Cost: 1

Path: Right


```python
easy_state = (1, 2, 3, 4, 5, 6, 7, 0, 8)

print("Misplaced Tiles:", misplaced_tiles(easy_state))
print("Manhattan Distance:", manhattan_distance(easy_state))

result = a_star_search(easy_state, manhattan_distance)
print("A* Result:", result)
```
Misplaced Tiles: 1

Manhattan Distance: 1

A* Cost: 1

A* Path: 'Right'
