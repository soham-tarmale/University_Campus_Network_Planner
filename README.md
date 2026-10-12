
# AOA_Mini_Project
AOA mini project (Prim's Algorithm)

# PBLE 1: Smart Delivery Planning – Fractional Knapsack

**Course:** Analysis of Algorithms (AOA)
**Language:** C
**Concepts covered:** Greedy Method, Fractional Knapsack, ratio-based selection, sorting, time-complexity analysis

## Problem Statement

A delivery company has a vehicle with a fixed carrying capacity. Each package has a weight and a value/profit. The vehicle can carry at most the given capacity. To maximize the total value, a complete package or a fraction of a package may be selected.

This program uses the Fractional Knapsack Greedy Algorithm to find the maximum possible value that can be carried.

## Algorithm (Greedy Method)

1. Calculate the value/weight ratio for every package.
2. Sort the packages in decreasing order of ratio.
3. Go through the sorted packages:
   - If the whole package fits in the remaining capacity, take it fully.
   - Otherwise, take only the fraction that fills the remaining capacity and stop.
4. Add up the value of everything taken to get the maximum value.

## Features

- Menu-driven program that runs until Exit is selected
- Uses arrays and functions
- Shows intermediate results (ratios and sorted order)
- Displays fraction taken, weight used and value gained for each selected package
- Handles invalid menu choices and invalid weights
- Menu options must be used in order (the program tells you which step is missing)

## Menu

1. Enter Package Details
2. Display Package Details
3. Calculate Value/Weight Ratio
4. Sort Packages by Ratio
5. Find Maximum Value
6. Display Selected Packages
7. Exit

## Input

- Number of packages
- Value/profit of each package
- Weight of each package
- Maximum carrying capacity of the vehicle

## How to Compile and Run

    gcc pble1_simple.c -o knapsack
    ./knapsack

On Windows (MinGW): `gcc pble1_simple.c -o knapsack.exe` then `knapsack.exe`

## Test Case

Input: 4 packages, vehicle capacity = 15

| Package | Value | Weight |
|---------|-------|--------|
| 1       | 40    | 5      |
| 2       | 30    | 10     |
| 3       | 50    | 5      |
| 4       | 20    | 4      |

Value/Weight ratios: 8, 3, 10, 5
Order after sorting: Package 3, 1, 4, 2

Output:

| Package | Fraction taken | Weight used | Value gained |
|---------|----------------|-------------|--------------|
| 3       | 1.00           | 5.00        | 50.00        |
| 1       | 1.00           | 5.00        | 40.00        |
| 4       | 1.00           | 4.00        | 20.00        |
| 2       | 0.10           | 1.00        | 3.00         |

Total weight used = 15.00
Maximum value = 113.00

## Time Complexity

- Calculating ratios: O(n)
- Sorting (bubble sort): O(n²)
- Greedy selection: O(n)
- **Overall: O(n²)**

Justification: Sorting is the most expensive step. Bubble sort compares pairs of packages in nested loops, so it takes O(n²). The ratio calculation and the selection each need one pass over the packages, which is O(n). With a faster sort such as merge sort or qsort, the overall complexity becomes O(n log n).

Space complexity: O(n) for the arrays that store package details.

## Files

- pble1_simple.c – C source code
- README.md – project description


