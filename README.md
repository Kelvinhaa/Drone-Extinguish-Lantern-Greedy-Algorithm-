# Drone Extinguish Lantern (Greedy Algorithm)

A C program that simulates drones moving on a 1D plane to eliminate lanterns at specific positions and arrival times.

This project currently implements Stage 1 (greedy assignment + trajectory simulation).

## What the Program Does

- Reads a simulation map from standard input.
- Assigns each lantern to a feasible drone using a greedy tie-breaking rule.
- Builds per-drone movement trajectories.
- Simulates time step by time step and prints elimination events.
- Prints summary results and each drone's assigned lantern path.

## Constraints in Code

- Plane width: positions 1..10
- Max drones: 10
- Max lanterns: 1000
- Max total time: 1000
- Drone speed: 1 position per time step

## Build

```bash
gcc -Wall -g -o lantern lantern.c -lm
```

## Run

Stage 1 is selected by passing argument `1`:

```bash
./lantern 1 < input.txt
```

If no/invalid stage is provided, usage is:

```text
Usage: <executable> <stage number>
e.g., lantern 1
```

## Input Format

Input must match this exact structure:

```text
Total time: <int>
Number of drones: <int>
Number of lanterns: <int>
Drones (starting location):
<drone_0_x>
<drone_1_x>
...
Lanterns (location, arrival time):
<lantern_0_x> <lantern_0_arrival_time>
<lantern_1_x> <lantern_1_arrival_time>
...
```

## Example Input

```text
Total time: 8
Number of drones: 2
Number of lanterns: 4
Drones (starting location):
2
8
Lanterns (location, arrival time):
3 1
7 2
4 3
8 4
```

## Example Output (Shape)

```text
At time 1 drone 0 eliminates lantern 0
At time 2 drone 1 eliminates lantern 1
...
Lanterns eliminated X of Y
Drone[0] lantern path: ...
Drone[1] lantern path: ...
```

## Greedy Assignment (Stage 1)

For each lantern in input order, choose among feasible drones using:

1. Minimum distance to lantern.
2. Earliest drone free time.
3. Smaller drone index.

A drone is feasible if it can reach the lantern by its arrival time.

## Notes

- Lantern elimination occurs when a drone is at the lantern position at the lantern arrival time.
- Drones are clamped to remain within plane bounds [1, 10].
- Input parsing is strict and will exit on malformed/out-of-bounds values.
