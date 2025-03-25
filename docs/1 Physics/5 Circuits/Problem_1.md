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
import matplotlib.pyplot as plt

def reduce_series(G):
    """Reduce series connections in the graph."""
    nodes_to_remove = [n for n in G.nodes if G.degree(n) == 2]
    for n in nodes_to_remove:
        if n in G:  # Check if node still exists
            neighbors = list(G.neighbors(n))
            if len(neighbors) == 2:  # Ensure still degree 2
                n1, n2 = neighbors
                # Get weights from edges data, handling potential KeyError
                edges_data = G.get_edge_data(n, n1)
                # Handle the case where the edge data is empty:
                R1 = edges_data[0]['weight'] if edges_data else 0  

                edges_data = G.get_edge_data(n, n2)
                # Handle the case where the edge data is empty:
                R2 = edges_data[0]['weight'] if edges_data else 0 

                G.remove_node(n)
                G.add_edge(n1, n2, weight=R1 + R2)
    return G

def reduce_parallel(G):
    """Reduce parallel connections in the graph."""
    edges_processed = set()
    for u in G.nodes:
        for v in G.nodes:
            if u < v and G.has_edge(u, v):
                edges = list(G[u][v].items())  # Get all edges between u and v
                if len(edges) > 1:  # Multiple edges indicate parallel resistors
                    R_values = [data['weight'] for _, data in edges]
                    R_parallel = 1 / sum(1/R for R in R_values)
                    G.remove_edges_from([(u, v)] * len(edges))  
                    G.add_edge(u, v, weight=R_parallel)
                    edges_processed.add((u, v))
    return G

def calculate_equivalent_resistance(G, source, sink):
    """Calculate equivalent resistance between source and sink."""
    G = G.copy()  # Work on a copy to preserve original graph
    while len(G.edges) > 1 or len(G.nodes) > 2:
        prev_edges = len(G.edges)
        G = reduce_series(G)
        G = reduce_parallel(G)
        if len(G.edges) == prev_edges:  # No reduction possible
            break
    if G.has_edge(source, sink):
        # Iterate through edges for MultiGraph:
        for _, data in G[source][sink].items():
            return data['weight']
    return float('inf')  # No path exists


def draw_graph(G, title):
    """Visualize the graph."""
    pos = nx.spring_layout(G)
    nx.draw(G, pos, with_labels=True, node_color='lightblue', node_size=500)
    labels = nx.get_edge_attributes(G, 'weight')
    nx.draw_networkx_edge_labels(G, pos, edge_labels=labels)
    plt.title(title)
    plt.show()

# Example 1: Simple Series Circuit
G1 = nx.MultiGraph()  # Use MultiGraph to allow parallel edges
G1.add_edge(0, 1, weight=2)
G1.add_edge(1, 2, weight=3)
print("Example 1 - Series (2Ω + 3Ω):")
print(f"Equivalent Resistance: {calculate_equivalent_resistance(G1, 0, 2)} Ω")
draw_graph(G1, "Simple Series Circuit")

# Example 2: Simple Parallel Circuit
G2 = nx.MultiGraph()
G2.add_edge(0, 1, weight=4)
G2.add_edge(0, 1, weight=4)  # Parallel resistors
print("\nExample 2 - Parallel (4Ω || 4Ω):")
print(f"Equivalent Resistance: {calculate_equivalent_resistance(G2, 0, 1)} Ω")
draw_graph(G2, "Simple Parallel Circuit")

# Example 3: Nested Configuration (Series with Parallel)
G3 = nx.MultiGraph()
G3.add_edge(0, 1, weight=2)       # 2Ω in series
G3.add_edge(1, 2, weight=3)       # 3Ω parallel
G3.add_edge(1, 2, weight=6)       # 6Ω parallel
G3.add_edge(2, 3, weight=1)       # 1Ω in series
print("\nExample 3 - Nested (2Ω + (3Ω || 6Ω) + 1Ω):")
print(f"Equivalent Resistance: {calculate_equivalent_resistance(G3, 0, 3)} Ω")
draw_graph(G3, "Nested Series-Parallel Circuit")
```
Example 1 - Series (2Ω + 3Ω):
Equivalent Resistance: 5 Ω
![image](https://github.com/user-attachments/assets/a88b4f64-9796-412c-b81f-c403c5be48bf)

Example 2 - Parallel (4Ω || 4Ω):
Equivalent Resistance: 2.0 Ω
![image](https://github.com/user-attachments/assets/73a608af-7597-45f2-8ef7-b80f655af444)

Example 3 - Nested (2Ω + (3Ω || 6Ω) + 1Ω):
Equivalent Resistance: 5.0 Ω
![image](https://github.com/user-attachments/assets/3ed63b6f-0f03-47a7-8c57-c394fb33be88)


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

