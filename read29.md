# Graphs

[source](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/graphs.html)

A graph is a non-linear data structure that can be looked at as a collection of vertices (or nodes) potentially connected by line segments named edges.

Here is some common terminology used when working with Graphs:

- Vertex - A vertex, also called a “node”, is a data object that can have zero or more adjacent vertices.
- Edge - An edge is a connection between two nodes.
- Neighbor - The neighbors of a node are its adjacent nodes, i.e., are connected via an edge.
- Degree - The degree of a vertex is the number of edges connected to that vertex.

Directed vs Undirected

Undirected Graphs

An Undirected Graph is a graph where each edge is undirected or bi-directional. This means that the undirected graph does not move in any direction.

For example, in the graph below, Node C is connected to Node A, Node E and Node B. There are no “directions” given to point to specific vertices. The connection is bi-directional.

![undirected graph](/images/graph1.png)

The undirected graph we are looking at has 6 vertices and 7 undirected edges.

Vertices/Nodes = {a,b,c,d,e,f}

Edges = {(a,c),(a,d),(b,c),(b,f),(c,e),(d,e),(e,f)}

Directed Graphs (Digraph)

A Directed Graph also called a Digraph is a graph where every edge is directed.

Unlike an undirected graph, a Digraph has direction. Each node is directed at another node with a specific requirement of what node should be referenced next.

Compare the visual below with the undirected graph above. Can you see the difference? The Digraph has arrows pointing to specific nodes.

![directed graph](/images/graph2.png)

The directed graph above has six vertices and eight directed edges

Vertices = {a,b,c,d,e,f}

Edges = {(a,c),(b,c),(b,f),(c,e),(d,a),(d,e)(e,c)(e,f)}

Complete vs Connected vs Disconnected
There are many different types of graphs. This depends on how connected the graphs are to other node/vertices.

The three different types are completed, connected, and disconnected.

Complete Graphs
A complete graph is when all nodes are connected to all other nodes.

Connected
A connected graph is graph that has all of vertices/nodes have at least one edge.

In the visual above, this looks a lot more than what you are used to seeing. If you look closely at the different vertices of the graph, you will see that each node is connected to at least one other node or vertices. A Tree is a form of a connected graph. We will talk more about that in a bit.

The disconnected graph shows that some nodes may not always be connected to other nodes or vertices of the graph. It is complelty possible to have standalone nodes or edges (also known as islands) in a graph data structure.

Graph Representation
We represent graphs through:

Adjacency Matrix
Adjacency List
We will represent the following graph as both an Adjacency Matrix and an Adjacency List:

![undirected graph](/images/graph1.png)

Adjacency Matrix
An Adjacency matrix is represented through a 2-dimensional array. If there are n vertices, then we are looking at an n x n Boolean matrix

Each Row and column represents each vertex of the data structure. The elements of both the column and the row must add up to 1 if there is an edge that connects the two, or zero if there isn’t a connection.

This is what an adjacency matrix looks like:

![adjacency matrix](/images/graph3.png)

A few things to note from the above:

1. Looking at the graph we are representing, you can see that Vertex A connects to both Vertex D and Vertex C. To show this, we place a 1 in the position of (a,c) and (a,d).
2. We follow this same pattern for the other vertex’s and where they are connected.
3. If there is not an edge/connection between the vertex’s, we represent this by placing a 0 in the appropriate point of the matrix.
a sparse graph is when there are very few connections. a dense graph is when there are many connections

Within an adjacency matrix, an undirected graph will always be symmetric. This is not the case for a directed graph.

Adjacency List
An adjacency list is the most common way to represent graphs.

An adjacency list is a collection of linked lists or array that lists all of the other vertices that are connected.

Adjacency lists make it easy to view if one vertices connects to another.

This is what an Adjacency List looks like:

![adjacency list](/images/graph4.png)

Looking at the original graph that we are representing, we can see that Vertex A has an edge to both Vertex C and Vertex D. As a result, we will place both Vertex C and Vertex D in the adjacency list. Just from observation, we can see that we will only place the vertices that are connected in the list. If there is no connection between the vertices, they are not listed.

Thinking about how we will implement this in code? Well, let’s look at what the visual is telling us.

1. We can visually see that we are working with a collection of some sort. The visual is depicting a Linked List, but you could easily make it an array of arrays if you’d like.
2. Each index or node (depending on the data structure you choose to represent the adjacency list) will be a vertex within the graph.
3. Every time you add an edge, you will find the appropriate vertices in the data structure and add it to the appropriate location.

Weighted Graphs
A weighted graph is a graph with numbers assigned to its edges. These numbers are called weights. This is what a weighted graph looks like:

![weighted graph](/images/graph5.png)

When representing a weighted graph in a matrix, you set the element in the 2D array to represent the actual weight between the two paths. If there is not a connection between the two vertices, you can put a 0, although it is known for some people to put the infinity sign instead.

Traversals
You will be required to traverse through a graph. The traversals itself are like those of trees. Below is a breakdown of how you would traverse a graph.

Breadth First
In a breadth first traversal, you are starting at a specific vertex/node. This node must be specified when calling the BreadthFirst() method. The breadth-first traversal of a graph is like that of a tree, with the exception that graphs can have cycles. Traversing a graph that has cycles will result in an infinite loop….this is bad. To prevent such behavior, we need to have some way to keep track of whether a vertex has been “visited” before. Upon each visit, we’ll add the previously-unvisited vertex to a visited set, so we know not to visit it again as traversal continues.

As a refresher of what breadth first actually means here it is: Breadth first traversal is when you visit all the nodes that are closest to the root as possible. From there you traverse outwards, level by level, until you have visited all the vertices/nodes.

Here is what the algorithm breadth first traversal looks like:

1. Enqueue the declared start node into the Queue.
2. Create a loop that will run while the node still has nodes present.
3. Dequeue the first node from the queue
if the Dequeue‘d node has unvisited child nodes, add the unvisited children to visited set and insert them into the queue.
4. Let’s look at a visual for a breadth first:

![breadth first graph](/images/graph6.png)

The visual above shows the levels in which the nodes will be added to the queue. You can see that since the root node is A, it will look the nodes that are only 1 away from the root. This is C,E, & B.

Next it will look at the nodes that are 2 away from the root, this is F, G, & D. It will follow this pattern until it reaches the end of the graph and all nodes have been visited.

Look at the code below to take a closer look at what is actually happening. This is the code for a breadth first traversal:

```py
ALGORITHM BreadthFirst(vertex)
    DECLARE nodes <-- new List()
    DECLARE breadth <-- new Queue()
    DECLARE visited <-- new Set()

    breadth.Enqueue(vertex)
    visited.Add(vertex)

    while (breadth is not empty)
        DECLARE front <-- breadth.Dequeue()
        nodes.Add(front)

        for each child in front.Children
            if(child is not visited)
                visited.Add(child)
                breadth.Enqueue(child)   

    return nodes
```

Here is a breakdown of what is going on:

1. We have declared that our starting node (or root) is going to be Node A.
2. The first thing we want to do is Enqueue the root.
3. We also need to add the root to the visited set.
4. Next, we enter a while loop. We want this loop to keep running until there are no more nodes in our queue.
5. Once we are in the while loop, we want to Dequeue the front node and then check to see if it has any children.
6. if there are children of the node we are currently looking at, we want to add them to visited set. This will help us know that we have already seen that node before, and won’t accidently push us into an infinite loop if the graph was cyclic. In addition to tracking each child node as visited, we want to place any of its children that have not yet been visited into the queue.
7. The process will complete until the queue is empty.
8. Once the while loop breaks, we can then return the list of nodes. This list will contain, in order, all the nodes that were traversed.

Depth First

In a depth first traversal, we approach it a bit different than the way we do when working with a depth first traversal of a tree. Similar to how the breadth-first uses a queue, we are going to use a Stack for our depth-first traversal.

The algorithm for a depth first traversal is as follows:

1. Push the root node into the stack
2. Start a while loop while the stack is not empty
3. Peek at the top node in the stack
4. If the top node has unvisited children, mark the top node as visited, and then Push any unvisited children back into the stack.
5. If the top node does not have any unvisited children, Pop that node off the stack
repeat until the stack is empty.
6. Let’s look at the visual for a depth-first traversal.
