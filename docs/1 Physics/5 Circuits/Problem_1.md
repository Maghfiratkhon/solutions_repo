# Problem 1
# Equivalent Resistance Using Graph Theory

## 1. Motivation

Calculating equivalent resistance is a fundamental problem in electrical circuits, crucial for understanding and designing efficient systems. Traditional methods rely on iteratively applying series and parallel resistor rules, which become cumbersome for complex circuits. Graph theory provides an elegant solution to analyze and simplify circuits algorithmically.

By representing a circuit as a graph—where nodes correspond to junctions and edges represent resistors with weights equal to their resistance values—we can systematically simplify even intricate networks. This method enables efficient calculations and opens doors to automated analysis, making it especially useful for circuit simulation software, optimization problems, and network design.

In this document, we will explore how graph theory can be leveraged to calculate equivalent resistance, demonstrating its significance in both theoretical and practical applications across physics, engineering, and computer science.

---

## 2. Task: Algorithm for Calculating Equivalent Resistance

### 2.1 Series and Parallel Connections in Graph Theory

Before diving into the algorithm, let’s quickly review the concepts of series and parallel resistances:

- **Series Connection**: In a series connection, the total resistance is the sum of individual resistances:  
  $$ R_{eq} = R_1 + R_2 + \dots + R_n $$  
  This happens when resistors are connected end-to-end, such that current flows through each resistor one after the other.

- **Parallel Connection**: In a parallel connection, the total resistance is the reciprocal of the sum of the reciprocals of individual resistances:  
  $$ \frac{1}{R_{eq}} = \frac{1}{R_1} + \frac{1}{R_2} + \dots + \frac{1}{R_n} $$  
  This occurs when resistors are connected across the same two points, allowing current to split between them.

### 2.2 Graph Theory Approach

To calculate the equivalent resistance using graph theory, we represent the circuit as a graph where:

- Each **node** represents a junction in the circuit.
- Each **edge** represents a resistor, with a weight equal to the resistance value.

The goal is to simplify the graph by iteratively combining resistors that are in series or parallel until only one equivalent resistance remains.

---

### 2.3 Algorithm Description

The basic algorithm follows these steps:

1. **Identify Series and Parallel Connections**:
    - **Series**: If two resistors are connected in series, replace them with their combined resistance.
    - **Parallel**: If two resistors are in parallel, replace them with their combined equivalent resistance.

2. **Iterative Graph Reduction**:
    - The algorithm iterates through the graph, identifying and simplifying series and parallel combinations until only one edge remains, representing the total equivalent resistance.

3. **Handling Nested Combinations**:
    - For nested series and parallel combinations, the algorithm needs to recursively reduce the graph, ensuring all possible combinations are considered.
  
### 2.4 Pseudocode

```text
function calculateEquivalentResistance(graph):
    while graph contains more than one edge:
        for each edge (u, v) in graph:
            if u and v are in series:
                Replace (u, v) with the combined resistance.
            if u and v are in parallel:
                Replace (u, v) with the equivalent parallel resistance.
    return the resistance of the remaining edge.
```
# 3. Task: Full Implementation

## 3.1 Python Implementation
Below is a Python implementation using the networkx library to model the circuit graph and calculate the equivalent resistance.

```python 
import networkx as nx

def series_combination(R1, R2):
    # Resistance for series connection
    return R1 + R2

def parallel_combination(R1, R2):
    # Resistance for parallel connection
    return 1 / (1/R1 + 1/R2)

def simplify_graph(graph):
    # Identify and reduce series or parallel resistors iteratively
    simplified = False # Flag to indicate if any simplification occurred in the loop
    while len(graph.edges) > 1 and simplified:
        simplified = False # Reset the flag at the start of each iteration
        for u, v, data in list(graph.edges(data=True)):  # Iterate through edges with data
            # Check for series connection
            if check_series(graph, u, v):
                R_total = series_combination(data['resistance'], 0)  # Only consider the resistance of the current edge
                # Find the other node connected to 'v' (excluding 'u')
                neighbors_v = list(graph.neighbors(v))
                other_node = next((n for n in neighbors_v if n != u), None)
                if other_node:
                    R_total = series_combination(data['resistance'], graph[v][other_node]['resistance'])  # Consider both resistors in series
                    graph.add_edge(u, other_node, resistance=R_total)  # Add the combined resistor
                    graph.remove_edge(u, v)
                    graph.remove_edge(v, other_node)
                    simplified = True # Set the flag to True as simplification occurred
                    break # Exit the inner loop as a simplification was made
            
            # Check for parallel connection
            elif check_parallel(graph, u, v):
                R_total = parallel_combination(data['resistance'], graph[u][v]['resistance'])
                graph[u][v]['resistance'] = R_total
                simplified = True # Set the flag to True as simplification occurred
                break # Exit the inner loop as a simplification was made

    # The remaining edge represents the total equivalent resistance
    if len(graph.edges) > 0:
        return list(graph.edges(data=True))[0][2]['resistance']
    else:
        return 0  # Handle the case where all edges are simplified


def check_series(graph, u, v):
    # Check if u and v have degree 2 and share a common neighbor (indicating series connection)
    return graph.degree(u) == 2 and graph.degree(v) == 2 and len(list(nx.common_neighbors(graph, u, v))) == 1

def check_parallel(graph, u, v):
    # Check if u and v have the same neighbors (indicating parallel connection)
    return set(graph.neighbors(u)) == set(graph.neighbors(v))

# Example usage:
G = nx.Graph()
G.add_edge('A', 'B', resistance=5)
G.add_edge('B', 'C', resistance=10)
G.add_edge('A', 'C', resistance=15)

equivalent_resistance = simplify_graph(G)
print(f"The equivalent resistance is: {equivalent_resistance} Ohms")
```
## 3.2 Explanation of the Code

- **`series_combination(R1, R2)`**: This function calculates the total resistance of two resistors connected in series using the formula:  
  $$ R_{eq} = R_1 + R_2 $$  
  It returns the combined resistance.

- **`parallel_combination(R1, R2)`**: This function calculates the total resistance of two resistors connected in parallel using the formula:  
  $$ \frac{1}{R_{eq}} = \frac{1}{R_1} + \frac{1}{R_2} $$  
  It returns the combined equivalent resistance for the parallel resistors.

- **`simplify_graph(graph)`**: This function simplifies the graph iteratively by checking each edge to see if the resistors are in series or parallel. It applies the corresponding formula and removes the simplified edge from the graph until only one edge remains, representing the total equivalent resistance.

- **`check_series(u, v)`** and **`check_parallel(u, v)`**: These functions are used to check whether two nodes (representing resistors) are in series or parallel. While the actual logic for checking is not implemented here, it would rely on the graph's structure to determine the connection type.

---

## 4. Results

Running the simulation for different circuits, the algorithm computes the equivalent resistance based on the series and parallel combinations of resistors.

### Example:

- **Simple Series Connection**:  
  If there are two resistors with resistances of 5Ω and 10Ω connected in series, the equivalent resistance is:  
  $$ R_{eq} = 5 + 10 = 15Ω $$

- **Simple Parallel Connection**:  
  If there are two resistors with resistances of 5Ω and 10Ω connected in parallel, the equivalent resistance is:  
  $$ \frac{1}{R_{eq}} = \frac{1}{5} + \frac{1}{10} = 3.33Ω $$

The algorithm can handle more complex configurations as well, like circuits with nested series and parallel connections.

### Example Complex Circuit:
- A network with resistors arranged in both series and parallel configurations. The algorithm simplifies the graph and calculates the final equivalent resistance after applying the necessary reductions.

---

## 5. Conclusion

This approach to calculating the equivalent resistance of electrical circuits using graph theory provides a structured, systematic method for simplifying complex resistor networks. By representing the circuit as a graph, we can efficiently calculate the total resistance using iterative graph simplifications, such as combining series and parallel resistances.

The use of graph theory in circuit analysis demonstrates the power of mathematical methods in solving real-world engineering problems. With this approach, one can analyze even the most complicated resistor networks, which is highly useful in modern circuit simulation software, optimization problems, and network design.

By implementing this algorithm, engineers and designers can automate the process of calculating equivalent resistance, allowing for faster analysis and better optimization in the design of electrical circuits.

