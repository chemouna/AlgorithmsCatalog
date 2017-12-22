

# Connected Components 

- In graph theory, a connected component (CC) of an undirected graph is a subgraph in which any two vertices are connected to each other by paths, and which is connected to no additional vertices in the graph. 

## Algorithms to find connected components

### BFS or DFS

### Using disjoint set Data Structure 


## CC in a Forest 


## CC in limited models of computation 

## Strongly CC

- a graph is said to be strongly connected or diconnected if every vertex is reachable from every other vertex 

### Algorithms 

#### DFS-based linear-time algorithms

##### Kosaraju's algorithm

- uses two passes of depth first search:
    - The first: in the original graph, is used to choose the order in which the outer loop of the second depth first search tests vertices for having been visited already and recursively explores them if not.
    - The second: is on the transpose graph of the original graph, and each recursive exploration finds a single new strongly connected component


##### Tarjan's strongly connected components algorithm 

##### Path-based strong component algorithm 

#### Reachability-based SCC algorithms

### Applications

#### Solve 2-satisfiability problems 

#### Dulmage–Mendelsohn decomposition

## Practice

### Questions 

#### How can the number of strongly connected components of a graph change if a new edge is added ?
- The number of strongly connected components can only decrease as the number of edges increase. 
     * If the edge is between two vertices that are already in the same strongly connected component, the number of components will not change. 
     * If the edge connects two vertices that belong to distinct scc’s, then the number of components will decrease by at most one.
