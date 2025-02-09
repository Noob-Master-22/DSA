# Breadth First Search Using Adjacency Matrix 

## BFS Algorithm
The general process of exploring a graph using breadth-first search includes the following steps:-

-Take the input for the adjacency matrix or adjacency list for the graph.  
-Initialize a queue.  
-Enqueue the root node (in other words, put the root node into the beginning of the queue).  
-Dequeue the head (or first element) of the queue, then enqueue all of its neighboring nodes, starting from left to right. If a node has no neighboring nodes which need to be explored, simply dequeue the head and continue the process.  
-(Note: If a neighbor which is already explored or in the queue appears, don’t enqueue it – simply skip it.)  
-Keep repeating this process till the queue is empty.  

```java
import java.util.LinkedList;
import java.util.Queue;


public class GraphBFSAdjMat {
    private int vertices; // Number of vertices in the graph
    private int[][] adjacencyMatrix; // Adjacency matrix to store graph edges

    // Constructor to create an empty graph
    public GraphBFSAdjMat(int v) {
        vertices = v;
        adjacencyMatrix = new int[v][v];
    }

    // Method to add an edge to the graph
    public void addEdge(int source, int destination) {
        adjacencyMatrix[source][destination] = 1;
        adjacencyMatrix[destination][source] = 1; // If the graph is undirected
    }

    // Method to perform BFS on the graph
    public void bfs(int start) {
        boolean[] visited = new boolean[vertices]; // Initialize all vertices as not visited
        Queue<Integer> queue = new LinkedList<>(); // Create a queue for BFS

        visited[start] = true; // Mark the starting vertex as visited
        queue.add(start); // Enqueue the starting vertex

        while (!queue.isEmpty()) {
            int current = queue.poll(); // Dequeue a vertex from the queue
            System.out.print(current + " ");

            for (int i = 0; i < vertices; i++) {
                if (adjacencyMatrix[current][i] == 1 && !visited[i]) {
                    visited[i] = true; // Mark the adjacent vertex as visited
                    queue.add(i); // Enqueue the adjacent vertex
                }
            }
        }
    }

    public static void main(String[] args) {
        // Create a new graph with 5 vertices
        GraphBFSAdjMat g = new GraphBFSAdjMat(5);

        // Add some edges to the graph
        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 2);
        g.addEdge(2, 0);
        g.addEdge(2, 3);
        g.addEdge(3, 3);

        // Perform BFS starting from vertex 2
        System.out.println("BFS:");
        g.bfs(2);
    }
}
```
## Time & Space Complexity


The running time complexity of the BFS in Java is O(V+E) where V is the number of nodes in the graph, and E is the number of edges.

Since the algorithm requires a queue for storing the nodes that need to be traversed at any point in time, the space complexity is O(V).
