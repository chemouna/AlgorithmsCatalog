

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

- Pseudo code: 
 1. For each vertex u of the graph, mark u as unvisited, L be empty
 2. For each vertex of the graph:
      if u is unvisited:
          visit(u) such that visit:
             1. Mark u as visited
             2. For each v out-neighbour of u: visit(v)
             3. prepend u to L 
 3. for each u in L: assign(u, u) such that assign(u, root):
      if u has not been assigned to a component:
         1. assign u as belonging to component whose root is root
         2. for each in-neighbour v of u: assign(v, root)
         
- [Implementation in java](https://github.com/chemouna/practice/blob/master/src/java/com/mounacheikhna/practice/graph/KosarajuScc.java)
- [Implementation in python](https://github.com/chemouna/AlgorithmsPy/blob/master/src/com/mounacheikhna/algorithms/graph/kosaraju.py)

##### Tarjan's strongly connected components algorithm 

##### Path-based strong component algorithm 

#### Reachability-based SCC algorithms

### Applications

#### Solve 2-satisfiability problems 

#### Dulmage–Mendelsohn decomposition

## Biconnected components
- Any connected graph decomposes into a tree of biconnected components called the block-cut tree of the graph. The blocks are attached to each other at shared vertices called cut vertices or articulation points. 

### Algorithms 

#### Linear time DFS 
- Algorithm: 
     run a depth-first search while maintaining the following information:
        - the depth of each vertex in the depth-first-search tree (once it gets visited), and
        - for each vertex v, the lowest depth of neighbors of all descendants of v (including v itself) in the depth-first-search tree, called the lowpoint.
   
 The lowpoint of v can be computed after visiting all descendants of v (i.e., just before v gets popped off the depth-first-search stack) as the minimum of the depth of v, 
 the depth of all neighbors of v (other than the parent of v in the depth-first-search tree) and the lowpoint of all children of v in the depth-first-search tree.

## Triconnected Components (SPQR tree)


## Summary
- Connected components is usually associated with undirected graphs (two way edges): there is a path between every two nodes.
- Strongly connected components is usually associated with directed graphs (one way edges): there is a route between every two nodes.
- Complete graphs are undirected graphs where there is an edge between every pair of nodes.

## Practice

### Questions 

#### How can the number of strongly connected components of a graph change if a new edge is added ?
- The number of strongly connected components can only decrease as the number of edges increase. 
     * If the edge is between two vertices that are already in the same strongly connected component, the number of components will not change. 
     * If the edge connects two vertices that belong to distinct scc’s, then the number of components will decrease by at most one.
