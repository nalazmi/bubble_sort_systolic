# Challenge #17: Sorting on a Systolic Array

This repository contains the solution for Challenge #17, focusing on understanding and analyzing the Bubble Sort algorithm, conceptually mapping it to a systolic array, and visualizing the performance of its sequential implementation.

## Overview

The challenge explores the Bubble Sort algorithm, its potential hardware implementation structure on a systolic array, and demonstrates its time complexity through software execution time measurements and visualization.

**Learning Goals:**

* Understand the basic principles of mapping an algorithm like Bubble Sort to a parallel architecture like a systolic array.
* Design (conceptually) a systolic array for sorting.
* Implement the sequential Bubble Sort algorithm in Python.
* Analyze and visualize the performance (execution time) of the sequential Bubble Sort as the input size increases.

## Challenge Tasks

1.  Design a systolic array that can do Bubble sort and determine its dimension.
2.  Code a software version of Bubble sort and test it.
3.  Visualize the execution times for various sorting sizes.

## Task 1: Systolic Array Design for Bubble Sort

**Concept:**
A systolic array processes data through a network of simple processing elements (PEs) in a rhythmic, pipeline-like fashion. To map Bubble Sort, which relies on adjacent comparisons and swaps, a linear array structure is suitable.

**Processing Element (PE):**
A core component for a systolic sorting array is a **compare-and-swap unit**. This PE takes two input values, compares them, and outputs the smaller value on one port and the larger value on the other.

Inputs: $A_{in}$, $B_{in}$
Operation: Compare $A_{in}$ and $B_{in}$.
Outputs: $A_{out} = \min(A_{in}, B_{in})$, $B_{out} = \max(A_{in}, B_{in})$ (The specific assignment of min/max to output ports depends on the data flow direction).

**Array Structure:**
A **1-dimensional linear array** of these compare-and-swap PEs is a natural fit for sorting a 1D list using a Bubble Sort-like process. Data items are fed into one end of the array and flow through the PEs.

**Dimension:**
The array needs to be **1-dimensional**.

**Size:**
To sort $N$ elements, the linear systolic array typically requires **$N$ processing elements**. As data streams through the $N$ PEs over multiple clock cycles, items are compared and ordered relative to their neighbors.

**Summary:** A 1-dimensional linear systolic array comprising $N$ compare-and-swap processing elements, designed for efficient parallel sorting of $N$ elements.

## Task 2: Software Implementation (Bubble Sort)

A standard sequential implementation of the Bubble Sort algorithm is provided in Python. This implementation serves as a basis for understanding the algorithm's logic and, importantly, for measuring its sequential time complexity.

The implementation is a direct translation of the algorithm: iterating through the list, comparing adjacent elements, and swapping them if they are out of order, repeating passes until the list is sorted.

```python
# Snippet showing the function signature
def bubble_sort(arr):
    """Implements the standard sequential Bubble Sort algorithm."""
    n = len(arr)
    # ... comparison and swap logic ...
```

## Task 3: Performance Measurement and Visualization

To analyze the performance of the Bubble Sort algorithm, the execution time of the sequential Python implementation was measured for various input sizes. Random lists of integers were generated for sizes ranging from 10 to 20,000 elements.

The results are visualized using `matplotlib`, plotting the input size against the execution time.

The plots demonstrate the relationship between the problem size and the time taken by the sequential Bubble Sort algorithm.

```python
# Snippet showing the plotting code (full code in the notebook)
import matplotlib.pyplot as plt
# ... (code to measure times) ...

# Plotting on a log-log scale
plt.figure(figsize=(10, 6))
plt.plot(sizes, execution_times, marker='o', linestyle='-')
plt.title('Bubble Sort Execution Time vs. Input Size (Sequential - Log Scale)')
plt.xlabel('Input Size (log scale)')
plt.ylabel('Execution Time (seconds - log scale)')
plt.xscale('log')
plt.yscale('log')
plt.grid(True, which="both", ls="--")
plt.show()

# Plotting on a linear scale
plt.figure(figsize=(10, 6))
plt.plot(sizes, execution_times, marker='o', linestyle='-')
plt.title('Bubble Sort Execution Time vs. Input Size (Sequential - Linear Scale)')
plt.xlabel('Input Size')
plt.ylabel('Execution Time (seconds)')
plt.grid(True)
plt.show()
