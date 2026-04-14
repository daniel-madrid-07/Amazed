# A-maze-d 🤖

**A pathfinding and robot coordination algorithm for maze solving** — An Epitech project implementing multi-robot path optimization.

## Overview

A-maze-d is a C-based project that solves complex maze routing problems by finding optimal paths for multiple robots navigating from a start room to an end room through an interconnected tunnel system. The program reads maze definitions, calculates shortest distances using BFS, and assigns robots to disjoint paths for efficient parallel traversal.

## Features

✨ **Core Functionality:**
- 📊 **Maze Parsing** - Parse room definitions and tunnel connections from standardized input format
- 🗺️ **Distance Calculation** - Compute shortest distances using Breadth-First Search (BFS)
- 🔀 **Path Extraction** - Extract multiple disjoint paths from start to end
- 🤖 **Robot Assignment** - Intelligently distribute robots across paths for optimization
- 🚀 **Robot Movement** - Simulate coordinated robot movement along assigned paths

## Architecture

```
A-maze-d/
├── src/                    # Main source files
│   ├── main.c             # Entry point and path handling
│   ├── parsing.c          # Input parsing and maze construction
│   ├── algo.c             # Path extraction algorithm
│   ├── calcul_distance.c  # BFS distance calculation
│   └── move_robots.c      # Robot movement simulation
├── include/
│   └── my.h               # Main header with data structures
├── lib/
│   ├── my_printf/         # Custom printf implementation
│   └── other_functions/   # Utility string and data functions
├── Makefile               # Build configuration
└── laby_gen.pl            # Maze generator utility
```

## Data Structures

### Core Types
- **room_t** - Represents a room with position, connections, and pathfinding metadata
- **tunnel_t** - Bidirectional connection between rooms
- **robot_t** - Individual robot with assigned path and position tracking
- **path_t** - Path structure with room sequence and robot assignments
- **queue_t** - BFS queue implementation for distance calculation

## Building

```bash
# Build the entire project
make

# Clean object files
make clean

# Remove all build artifacts
make fclean

# Rebuild from scratch
make re

# Build with debug symbols
make debug
```

### Requirements
- **Compiler**: clang (C99+)
- **Dependencies**: 
  - CSFML libraries (graphics, system, audio, window)
  - libm (math library)
  - Standard C libraries

## Usage

```bash
# Run the program with maze input
./amazed < maze_input.txt
```

### Input Format

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

### Output Format

The program outputs:
1. Original input (rooms and tunnels)
2. Robot movements in format: `G-<robot_id>-<next_room>`
3. One step per line until all robots reach the end room

## Algorithm Details

### 1. Parsing Phase
- Reads maze definition from stdin
- Builds room graph with bidirectional tunnels
- Identifies start (##start) and end (##end) marked rooms

### 2. Distance Calculation (BFS)
- Computes shortest distance from every room to the end room
- Stores distance values for pathfinding heuristics

### 3. Path Extraction
- Finds multiple disjoint paths from start to end
- Uses greedy algorithm to extract paths by always moving toward rooms with decreasing distance values
- Marks visited rooms to avoid path overlap

### 4. Robot Assignment
- Distributes robots across available paths
- Optimizes by assigning multiple robots to longer paths when beneficial

### 5. Movement Simulation
- Executes robots in parallel along their assigned paths
- Coordinates movement to avoid collisions
- Continues until all robots reach the end room

## Project Stats

- **Lines of Code**: ~517 (main source)
- **Project Size**: ~600KB (with libraries)
- **Language**: C (C99 standard)
- **Build System**: Make

## Notes

- The project includes custom implementations of `my_printf` and common string utilities (`my_strlen`, `my_strcpy`, etc.)
- The BFS-based distance calculation ensures optimal pathfinding
- Robot path assignment uses a greedy distribution strategy for multi-robot scenarios
- The program handles edge cases like missing start/end rooms and disconnected start/end

## License

Part of Epitech curriculum projects (2026).

---

**Project Type**: Algorithm & Data Structures  
**Difficulty**: Intermediate  
**Key Concepts**: Graph Algorithms, Pathfinding, BFS, Dynamic Memory Management
