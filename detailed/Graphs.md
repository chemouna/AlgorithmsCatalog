
# Graphs 

## Types of graphs

### Clique graph
 
### De Bruijn graph

### Petersen graph
- is an undirected graph with 10 vertices and 15 edges. It is a small graph that serves as a useful example and counterexample for many problems in graph theory.

### Planar graph
 
### Split graph
- a split graph is a graph in which the vertices can be partitioned into a clique and an independent set. 

## Paths 

### Simple Path 
- A path that does not repeat vertices is called a simple path. 

### Open Path
- is a path starts and ends at different vertices 

### Closed Path
- is a path that starts and ends at the same vertex

### Induced Path
- an induced path in an undirected graph G is a path that is an induced subgraph of G. That is, it is a sequence of vertices in G such that each two adjacent vertices in 
  the sequence are connected by an edge in G, and each two nonadjacent vertices in the sequence are not connected by any edge in G. An induced path is sometimes called a snake \

### Hamiltonian path
- is a path in an undirected or directed graph that visits each vertex exactly once. A Hamiltonian cycle (or Hamiltonian circuit) is a Hamiltonian path that is a cycle.

## Dominator 
- a node d dominates a node n if every path from the entry node to n must go through d. Notationally, this is written as d dom n (or sometimes d >> n). 
  By definition, every node dominates itself. 


## Articulation Points (Cut Vertices)
- a cut vertex is any vertex whose removal increases the number of connected components. 

## Bridge (Cut edge)
- is an edge of a graph whose deletion increases its number of connected components.[1] Equivalently, an edge is a bridge if and only if it is not contained in any cycle. 
- A graph with n nodes can contain at most {\displaystyle n-1} n-1 bridges, since adding additional edges must create a cycle. The graphs with exactly n-1 bridges are 
  exactly the trees, and the graphs in which every edge is a bridge are exactly the forests. 

### Algorithms 

#### Tarjan's Bridge-finding algorithm 

#### Bridge-Finding with Chain Decompositions 

