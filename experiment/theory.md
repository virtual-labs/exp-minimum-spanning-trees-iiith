Lets look at a simple method to find the MST of a given graph G. We start with a spanning graph of G with no edges initially and keep adding edges one by one. As we want to minimize the total cost, we should prefer to add edges with smaller weights first, but should not add edges that create cycles. This method of greedily picking the edges to form a MST is called the Kruskal's algorithm, and is described below.  

**Algorithm Kruskals(G)**
*sort the edges of G in increasing order of weight as e1, e2, ..., em
i = 1; E(T) = Φ
while |E(T)| < n-1 do
if E(T) ∪ ei does not have a cycle then
E(T) = E(T) ∪ ei
end-if
i = i + 1;
end-while*
**End-Kruskals**  

We still need to implement the cycle checker. The simplest way to do this is as follows. Suppose we want to check if adding a edge (u,v) can create a cycle or not. Before adding the edge (u,v), perform a depth first search (DFS) starting from v to see if the vertex u can be reached from v. If it can be reached, then adding (u,v) will create a cycle. The time taken for DFS is O(m+n) and for a tree m = O(n), so the running time is O(n). In the worst case, we need to try all m edges, so the running time of Kruskal's algorithms if we use a simple cycle checker is O(mn). Using some advanced datastructures, we can bring down the running time to O(m log n). We will now look at a much simpler solution with smaller runtime, using basic data structures.  

In this approach, we maintain a single tree T at any time. In each iteration, T is extended by adding one vertex v not in T and one edge from v to some vertex in T. Starting from a tree of one node, this process is repeated (n-1) times. For each vertex v in G, there must be at least one edge in any MST. Considering the edge of the smallest weight is useful as it can decrease the cost of the spanning tree. So, for any vertex v, the edge with the least weight among all edges having one of its end points as v, is always contanied in any MST of G. Let T is a subtree of some MST of an undirected weighted graph T. Consider edges (u,v) in G such that u is in T and v is not in T. Of all such edges, let e = (x,y) be the edge with the smallest weight. Then T ∩ {e} is also a subtree of some MST of G. This suggests an incemental method of constructing a MST. This algorithm is called Prim's algorithm, and is described below.  

**Algorithm Prims(G,v)**
*Add v to T;
While T has less than n − 1 edges do
w = vertex s.t. (v,w) has the smallest weight amongst edges with one endpoint in T and another not in T.
Add (v,w) to T.
end-while*
**End-Prims**

The only thing left is to efficiently find the vertex w in the above algorithm. For this purpose, we associate a key to every vertex and key[v] is the smallest weight of edges with v as one endpoint and another in the current tree T. A key[v] changes only when some vertex is added to T and also vertex with the smallest key[v] is the one to be added to T. When a vertex is added to T, only its neighboring vertices may have to update their keys. Therefore, we can maintain a heap of vertices with their key[] values and perform the above algorithm as follows.  

**Algorithm Prims_heap(G, u)**
*for each vertex v do key[v] = ∞
key[u] = 0;
Add all vertices to a heap H.
While T has less than n-1 edges do
v = deleteMin();
Add v to T via uv s.t. u is in T
For each neighbor w of v do
if W(vw) > key[w] then DecreaseKey(w)
end-for
end-while*
**End-Prims_heap**

Runtime: Each vertex is deleted once from the heap. Each DeleteMin() takes O(log n) time. So, this accounts for a time of O(n log n). Each edge may result in one call to DecreaseKey(). Over m edges, this accounts for a time of O(m log n). Total time = *O((n+m)log n)*.


