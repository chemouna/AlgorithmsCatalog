
# Graphs 

## Types of graphs

### Clique graph
 
### De Bruijn graph

### Petersen graph
- is an undirected graph with 10 vertices and 15 edges. It is a small graph that serves as a useful example and counterexample for many problems in graph theory.

### Planar graph
 
### Split graph
- a split graph is a graph in which the vertices can be partitioned into a clique and an independent set. 

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

