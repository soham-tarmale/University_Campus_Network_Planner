
# AOA_Mini_Project
AOA mini project (Prim's Algorithm)

# University Campus Network Planner using Prim's Algorithm


**Mini Project 12**

**Module 3:** Greedy Method Approach

**Related AOA Topic:** Minimum-Cost Spanning Tree, Prim's Algorithm


A menu-driven C program that plans the cheapest possible network connecting all buildings of a university campus.

The campus is modelled as a weighted undirected graph, and the network is found using Prim's greedy algorithm.


---


## Table of Contents

1. Problem Statement

2. Objective

3. Concepts Used

4. Input and Output

5. Algorithm

6. Worked Example

7. Data Structures

8. Program Structure

9. Menu Guide

10. How to Compile and Run

11. Sample Run

12. Disconnected Graph Demo

13. Complexity Analysis


---


## 1. Problem Statement

A university campus has several buildings, such as the Library, Admin Block, Computer Science Department, Hostel and Canteen.

Network cable can be laid between some pairs of buildings, and each possible link has an installation cost.

The university wants every building connected to the network at the **lowest total cost**, without laying any unnecessary cable.


---


## 2. Objective

- Implement Prim's greedy choice: starting from a selected building, repeatedly choose the cheapest edge that connects an already reached building to an unreached one.

- Produce a Minimum Spanning Tree (MST) from a connected weighted graph.

- Compare the results obtained from different starting buildings.


---


## 3. Concepts Used

| Concept | Role in this project |
|---|---|
| Graph | Buildings are vertices, possible cable links are edges |
| Weighted undirected graph | Edge weight is the installation cost; a link works in both directions |
| Spanning tree | A set of links that connects all buildings with no cycles |
| Minimum spanning tree | The spanning tree with the smallest total cost |
| Greedy method | At every step, take the cheapest edge that grows the tree |
| Adjacency matrix | Stores the cost between every pair of buildings |


---


## 4. Input and Output

### Input

- Number of buildings and their names (one word each)

- Connection costs between pairs of buildings (positive integers)

- Starting building for Prim's algorithm


### Output

- Order in which buildings are selected

- MST connections in `parent - child : cost` form

- Total installation cost

- A warning if the graph is disconnected

- Total cost from every possible starting building (comparison)


---


## 5. Algorithm

**Step 1: Create the graph.**
Store the weighted undirected graph in `cost[][]`. A value of `0` means no direct link.


**Step 2: Initialize.**
Set `key[i] = INF`, `parent[i] = -1` and `visited[i] = 0` for all buildings. Set `key[start] = 0`.


**Step 3: Select.**
Repeat up to `n` times: pick the unvisited building `u` with the smallest `key`. Mark it visited and add `key[u]` to the total cost.
If no unvisited building has a finite key, stop, because the rest are unreachable.


**Step 4: Update neighbours.**
For every unvisited building `v` that has a link to `u`, if `cost[u][v] < key[v]`, set `key[v] = cost[u][v]` and `parent[v] = u`.


**Step 5: Print.**
Show the selection order, each MST edge (`parent[v] - v`) with its cost, and the total cost.


**Step 6: Validate.**
If fewer than `n` buildings were reached, print a disconnected-graph warning.


### Why it works (greedy choice)

At every step, the cheapest edge leaving the set of already connected buildings is always safe to add to some minimum spanning tree (the cut property).

Repeating this choice until all buildings are covered gives an MST.


---


## 6. Worked Example

### Sample campus (menu option 6)

Buildings: `1 Library`, `2 Admin`, `3 CSDept`, `4 Hostel`, `5 Canteen`


| Link | Cost |
|---|---|
| Library - Admin | 4 |
| Library - CSDept | 3 |
| Admin - CSDept | 1 |
| Admin - Hostel | 2 |
| CSDept - Hostel | 4 |
| Hostel - Canteen | 2 |


### Cost matrix

```
           Lib   Adm   CSD   Hos   Can

Library     0     4     3     0     0

Admin       4     0     1     2     0

CSDept      3     1     0     4     0

Hostel      0     2     4     0     2

Canteen     0     0     0     2     0
```


### Trace, starting from Library

| Step | Selected | key[] after update (Lib, Adm, CSD, Hos, Can) | Edge added | Running cost |
|---|---|---|---|---|
| 1 | Library | 0, 4, 3, INF, INF | none (start) | 0 |
| 2 | CSDept (key 3) | 0, 1, 3, 4, INF | Library - CSDept (3) | 3 |
| 3 | Admin (key 1) | 0, 1, 3, 2, INF | CSDept - Admin (1) | 4 |
| 4 | Hostel (key 2) | 0, 1, 3, 2, 2 | Admin - Hostel (2) | 6 |
| 5 | Canteen (key 2) | 0, 1, 3, 2, 2 | Hostel - Canteen (2) | 8 |


**Result:** MST total cost = **8**, using 4 links for 5 buildings (a spanning tree always has `n - 1` edges).


Notice step 3: Admin was first reached through Library at cost 4, but once CSDept joined the tree, the cheaper link CSDept - Admin (cost 1) replaced it.

This is exactly what the "update neighbours" step does.


---


## 7. Data Structures

| Variable | Type | Purpose |
|---|---|---|
| `names[MAX][30]` | char array | Building names |
| `cost[MAX][MAX]` | int matrix | Link cost between each pair, `0` = no link |
| `n` | int | Number of buildings |
| `key[]` | int array | Cheapest known link cost connecting each building to the tree |
| `parent[]` | int array | Building through which each building is connected |
| `visited[]` | int array | Whether a building is already in the tree |


**Constants:**

- `MAX = 20` (maximum buildings)

- `INF = 9999` (stands for "not reachable yet")


---


## 8. Program Structure

| Function | What it does |
|---|---|
| `addBuildings()` | Reads the number of buildings and their names, and clears the cost matrix |
| `addConnection()` | Reads two building numbers and a cost, and stores it symmetrically |
| `showMatrix()` | Prints the cost matrix with building names |
| `prim(start, show)` | Runs Prim's algorithm and returns the total cost. If `show` is 1, it also prints selection order and MST edges |
| `runPrim()` | Asks for a starting building and calls `prim()` with printing on |
| `compareStarts()` | Calls `prim()` from every building and prints each total cost |
| `loadSample()` | Loads the 5-building sample campus |
| `main()` | Displays the menu in a `do...while` loop and dispatches with `switch` |


---


## 9. Menu Guide

| No. | Option | Notes |
|---|---|---|
| 1 | Enter buildings | Resets any existing graph |
| 2 | Add connection | Enter building 1, building 2 and cost on one line, e.g. `1 3 5` |
| 3 | Show cost matrix | `0` means no direct link |
| 4 | Run Prim's algorithm | Shows selection order, MST edges, total cost |
| 5 | Compare different starting buildings | Total cost from each starting point |
| 6 | Load sample data | Quick demo with the 5-building campus |
| 0 | Exit | |


**Typical flow for your own data:**

1. Option 1 to enter the buildings.

2. Option 2 once for each link.

3. Option 3 to check the matrix.

4. Option 4 to run Prim's algorithm.


---


## 10. How to Compile and Run

Requires a C compiler such as GCC.


```
gcc campus_simple.c -o campus_simple


./campus_simple            (Linux / macOS / WSL)

.\campus_simple            (Windows PowerShell)
```


If Windows blocks the compiled `.exe` ("Application Control policy has blocked this file"), compile and run from a different folder such as `C:\dev`, or use WSL or an online C compiler.


---


## 11. Sample Run

Inputs are shown after `>`. Repeated menu text is omitted.


```
Choice: > 6

Sample loaded.



Choice: > 4

1. Library
2. Admin
3. CSDept
4. Hostel
5. Canteen

Start from building number: > 1


Selected: Library
Selected: CSDept
Selected: Admin
Selected: Hostel
Selected: Canteen


MST connections:

CSDept - Admin : 1
Library - CSDept : 3
Admin - Hostel : 2
Hostel - Canteen : 2

Total cost = 8



Choice: > 5

Start Library -> total cost 8
Start Admin -> total cost 8
Start CSDept -> total cost 8
Start Hostel -> total cost 8
Start Canteen -> total cost 8
```


**Observation:** the MST cost is the same (8) from every starting building. The order of selection and the way edges are listed can change with the starting point, but the minimum total cost does not.

MST connections are listed in building-number order, not in selection order, so the first line printed may not be the first edge added.


---


## 12. Disconnected Graph Demo

**Setup:**

1. Choose option 1 and enter 3 buildings: `A`, `B`, `C`.

2. Choose option 2 and add only one link: `1 2 5`.

3. Choose option 4 and start from building 1.


**Expected result:**

```
Selected: A
Selected: B


MST connections:

A - B : 5

Total cost = 5


WARNING: Graph is disconnected! Not all buildings are connected.
```


Building C has no link to the others, so it can never be reached.

The program stops selecting, prints the part of the tree it could build, and warns the user.


---


## 13. Complexity Analysis

| Measure | Value | Reason |
|---|---|---|
| Time | O(V^2) | `n` rounds, each scanning all vertices to find the minimum key and to update neighbours |
| Space | O(V^2) | The adjacency matrix. The `key`, `parent` and `visited` arrays add only O(V) |


With a min-heap and an adjacency list, Prim's can be improved to O(E log V), which is better for sparse graphs.

For a campus with a few dozen buildings, the matrix version is simple and fast enough.


---







---


**Subject:** Analysis of Algorithms (AOA)

**Language:** C

