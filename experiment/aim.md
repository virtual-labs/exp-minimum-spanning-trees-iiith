

In this experiment, we will see a famous problem in graphs, finding the Minimum Spanning Tree. Let G = (V, E, W) be a weighted graph. Find a subgraph G' of G that is connected and has the smallest cost, where cost is defined as the sum of the edge weights of all edges in G'. Observe that if G' has a cycle, we can remove one of the edges along a cycle and still the resultant graph will remain connected and has smaller cost than G'. Hence, G' cannot be have a cycle and as it has to be connected, G' must be a tree. We define G' as a spanning subgraph of G iff V(G) = V(G') and a spanning subgraph that is also a tree is called a spanning tree of G. Our aim is to find a spanning tree of G that has the least cost and such a spanning tree is called as minimum spanning tree (MST) of G.

