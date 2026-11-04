# Stepwise

An interactive visualizer for sorting and pathfinding algorithms. Watch each algorithm work one step at a time, with live counts of the work it does.

**Live demo:** `https://anred-netizen.github.io/stepwise/`

## Features

### Sorting
- Bubble, insertion, selection, merge, quick and heap sort
- Input types: random, nearly sorted, reversed, few unique values
- Live counters for comparisons and array writes
- Final result is checked against a sortedness test before the bars turn green
- Reset restores the same input, so you can compare algorithms on identical data

### Pathfinding
- A*, Dijkstra, breadth-first, depth-first and greedy best-first search
- Draw walls and "mud" (cost 5), drag the start and goal, generate a random maze or random walls
- Dijkstra and A* find the lowest-cost route around mud; BFS and DFS ignore cell cost
- **Compare all five** runs every algorithm on your current board and shows cells explored, path length, path cost and compute time

## How it works

Every algorithm is a JavaScript generator (`function*`) that yields one event per comparison, swap, write or visited cell. The renderer consumes those events at a speed the user controls. Because the algorithms never touch the canvas, pause, step and speed control work the same way for all of them.

| Piece | Implementation |
|---|---|
| Rendering | Canvas 2D, redrawn from the current state each frame |
| Algorithms | Generator functions yielding step events |
| Priority queue | Binary min-heap used by Dijkstra, A* and greedy search |
| A* heuristic | Manhattan distance (admissible, since the cheapest cell costs 1) |
| Maze | Randomized depth-first carving on an odd-sized grid |
| Theming | CSS custom properties, follows the system light/dark setting |
| Dependencies | None |

## Complexity reference

| Sort | Best | Average | Worst | Space | Stable |
|---|---|---|---|---|---|
| Bubble | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Insertion | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Selection | O(n²) | O(n²) | O(n²) | O(1) | No |
| Merge | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quick | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| Heap | O(n log n) | O(n log n) | O(n log n) | O(1) | No |

| Search | Time | Shortest path | Uses mud cost |
|---|---|---|---|
| BFS | O(V + E) | Fewest steps | No |
| DFS | O(V + E) | No | No |
| Dijkstra | O((V + E) log V) | Yes | Yes |
| A* | Depends on heuristic | Yes | Yes |
| Greedy best-first | O(E log V) | No | No |

## Run locally

No build step. Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```

## Ideas for next steps

- Bidirectional search and Jump Point Search
- Diagonal movement with a matching heuristic
- Sound feedback tied to comparisons
- Shell sort, radix sort and Timsort
- Save and share boards via the URL

## License

MIT
