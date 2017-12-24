
# DFS 
is an algorithm for traversing or searching tree or graph data structures. One starts at the root (selecting some arbitrary node as the root in the case of a graph) 
and explores as far as possible along each branch before backtracking.

DFS output can be described in terms of a spanning tree of the vertices reached during the search. Based on this spanning tree, the edges of the original graph can 
be divided into three classes: forward edges, which point from a node of the tree to one of its descendants, back edges, which point from a node to one of its ancestors, 
and cross edges, which do neither. Sometimes tree edges, edges which belong to the spanning tree itself, are classified separately from forward edges. If the original 
graph is undirected then all of its edges are tree edges or back edges. 


## DFS Forests 

- A DFS starting at some vertex v explores the graph by building up a tree that contains all vertices that are reachable from v and all edges that are used to reach these vertices. 
  We call this tree a DFS tree. A complete DFS exploring the full graph (and not only the part reachable from a given vertex v) builds up a collection of trees, or forest, 
  called a DFS forest.

## DFS and Spanning Trees 
- if the search is depth-first, each edge (v, w) not in the spanning tree connects vertex v with one of its ancestors w. 

## DFS variants

### Iterative Deepening Depth First Search

## Applications of DFS

### Strong Connectivity

### Directed Acyclic Graphs 
Checking if a graph is acyclic can be done in linear time with DFS

### Topological Order
ordering vertices by descreasing finish times computed by DFS is a valid topological order.

### Longest Path 
longest paths in a DAG can be computed in linear time using DFSi
