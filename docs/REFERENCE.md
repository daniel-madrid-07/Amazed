# Amazed — technical reference

## Architecture

```
Amazed/
├── src/                    # Main source files
│   ├── main.c             # Entry point and path handling
│   ├── parsing.c          # Input parsing and maze construction
│   ├── algo.c              # Path extraction algorithm
│   ├── calcul_distance.c  # BFS distance calculation
│   └── move_robots.c      # Robot movement simulation
├── include/
│   └── my.h                # Main header with data structures
├── lib/
│   ├── my_printf/          # Custom printf implementation
│   └── other_functions/    # Utility string and data functions
├── Makefile                 # Build configuration
└── laby_gen.pl              # Maze generator utility
```

### Core data types

- **room_t** — represents a room with position, connections, and pathfinding metadata
- **tunnel_t** — bidirectional connection between rooms
- **robot_t** — individual robot with assigned path and position tracking
- **path_t** — path structure with room sequence and robot assignments
- **queue_t** — BFS queue implementation for distance calculation

## Input format

```
<number_of_robots>
<room_name> <x_pos> <y_pos>
##start
<start_room_name> <x> <y>
<other_room_name> <x> <y>
##end
<end_room_name> <x> <y>
<room_name>-<connected_room>
```

## Output format

The program outputs:
1. Original input (rooms and tunnels)
2. Robot movements in format: `G-<robot_id>-<next_room>`
3. One step per line until all robots reach the end room

## Algorithm details

1. **Parsing phase** — reads maze definition from stdin, builds room graph with bidirectional tunnels, identifies start (`##start`) and end (`##end`) marked rooms
2. **Distance calculation (BFS)** — computes shortest distance from every room to the end room, stores distance values for pathfinding heuristics
3. **Path extraction** — finds multiple disjoint paths from start to end using a greedy algorithm that always moves toward rooms with decreasing distance values, marking visited rooms to avoid path overlap
4. **Robot assignment** — distributes robots across available paths, assigning multiple robots to longer paths when beneficial
5. **Movement simulation** — executes robots in parallel along their assigned paths, coordinating movement to avoid collisions until all robots reach the end room

## Notes

- The project includes custom implementations of `my_printf` and common string utilities (`my_strlen`, `my_strcpy`, etc.)
- The BFS-based distance calculation ensures optimal pathfinding
- Robot path assignment uses a greedy distribution strategy for multi-robot scenarios
- The program handles edge cases like missing start/end rooms and disconnected start/end
