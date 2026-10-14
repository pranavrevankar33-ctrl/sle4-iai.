# sle4-iai.
# IAI-SLE
# SLE-4: Architecture Decision Record (ADR) - BFS vs DFS on the 8-Puzzle
A short document that records one important design decision from this project, explains why it was made, and defends it with real profiling numbers from SLE-2 and the C4 design from SLE-3.

## Overview

* Decision recorded: use of Breadth-First Search (FIFO queue + visited set) as the primary 8-puzzle solving strategy
* Alternatives considered: DFS (implemented and profiled), A* with Manhattan-distance heuristic (future upgrade), Iterative Deepening DFS (considered only)
* Backed by: SLE-2 profiling numbers and SLE-3 C4 architecture diagrams

## Technologies / References Used

* Python 3
* `collections.deque` (BFS Frontier) vs list (DFS Frontier)
* `time.perf_counter()` and `cProfile` (from SLE-2 profiling)
* C4 model: Context, Container, Component, Code (from SLE-3)

## Project Structure

```
IAI-SLE/
|
|-- agent.py
|-- ai-profiling.py
|-- SLE3_25UAM087_PranavRevankar.docx
|-- SLE4_25UAM087_PranavRevankar.docx
`-- README.md

```

## How to Read

1. Clone the repository

```
git clone https://github.com/pranavrevankar33-ctrl/IAI-SLE.git
```

2. Navigate to the project folder

```
cd IAI-SLE
```

3. Open `SLE4_25UAM087_PranavRevankar.docx` to read the full ADR, or see the summary below.

## Decision Summary

```
Title     : Use of BFS (FIFO Queue + Visited Set) as the Primary 8-Puzzle Solving Strategy
Status    : Accepted
BFS Time  : 12.494 ms   |   DFS Time  : 342.052 ms   (BFS ~27.4x faster)
BFS Nodes : 6,027        |   DFS Nodes : 129,832       (BFS ~21.5x fewer)
Reachable states explored: BFS 3.3%  |  DFS 71.6%  (of 181,440 total)

```

## How It Works

The ADR follows the standard format: Context (why a decision was needed), Decision (what was chosen), Alternatives Considered (DFS, A*, IDDFS), Rationale (backed by the SLE-2 table and SLE-3 diagrams), and Consequences (positive and negative trade-offs).

* **Context:** BFS and DFS behave very differently on the same 8-puzzle, so one had to be chosen as the system's primary strategy.
* **Decision:** BFS was chosen as primary; DFS is kept only as a baseline for comparison.
* **Rationale:** BFS was about 27.4x faster, expanded about 21.5x fewer nodes, and guarantees the shortest solution, while DFS gives no such guarantee.
* **Consequences:** BFS is optimal and simple to justify, but it uses more memory and is uninformed, so A* would likely do even better on a larger puzzle.

## Learning Objectives
This document is useful for anyone who wants to learn:

* How to write an Architecture Decision Record (ADR)
* How to justify a design choice using real profiling data, not just theory
* How BFS and DFS trade off speed, memory and solution quality
* How SLE-2 (profiling) and SLE-3 (C4 architecture) connect to a final design decision

## Future Improvements
Some possible improvements include:

* Implement A* with a Manhattan-distance heuristic and record a second ADR comparing it to BFS
* Test the decision on multiple start states, not just one
* Add a priority-queue-based Frontier as a new alternative
* Record further ADRs for other decisions made across SLE-1 to SLE-3

## Author
Pranav Gajanan Revankar
If you found this project useful, consider giving the repository a star.
