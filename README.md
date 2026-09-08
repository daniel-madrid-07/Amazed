<div align="center">

# Amazed

**A pathfinding and multi-robot coordination algorithm for maze solving.**

</div>

---

## What it does

Amazed solves maze routing problems by finding optimal paths for multiple robots navigating from a
start room to an end room through an interconnected tunnel system. It reads a maze definition,
calculates shortest distances with BFS, and assigns robots to disjoint paths for efficient
parallel traversal.

## Features

- **Maze parsing** — reads room definitions and tunnel connections from a standardized input format
- **Shortest-path calculation** — breadth-first search from every room to the end room
- **Disjoint path extraction** — finds multiple non-overlapping paths from start to end
- **Robot assignment & simulation** — distributes robots across paths and simulates coordinated, collision-free movement

## Installation / Usage

```bash
make                       # Build
./amazed < maze_input.txt  # Run with a maze definition
```

Requires a C99 compiler (clang) and the CSFML libraries. Input/output format and algorithm
breakdown: **[docs/REFERENCE.md](docs/REFERENCE.md)**.

## Tech stack

C (C99), CSFML, Make, Perl (maze generator script)

## License

School project — see [LICENSE](LICENSE)
