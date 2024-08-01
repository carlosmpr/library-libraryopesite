---
  title: 'PythonTestFile.py'
  description: 'component description'
  pubDate: 'August 1, 2024'
  author: 'Carlos Polanco'
  ---
  
  
  
  # PythonTestFile.py
  # Explanation of Shortest Path Algorithm using Dijkstra's Algorithm

This code implements a graph data structure and a method to find the shortest path between two nodes using Dijkstra's algorithm. Here's a breakdown of the code:

### Graph Class
- The `Graph` class represents a graph data structure.
- `__init__` method initializes the graph with an empty dictionary to store nodes and their neighbors.
- `add_node` method adds a node to the graph with its neighbors.

### Shortest Path Method
- `shortest_path` method finds the shortest path between two nodes in the graph using Dijkstra's algorithm.
- It initializes a priority queue `queue` with the starting node and its cost.
- Initializes dictionaries `distances` and `previous` to store the distance from the start node and the previous node in the path.
- Uses a set `visited` to keep track of visited nodes.
- While the queue is not empty, it dequeues the node with the lowest cost.
- For each neighbor of the current node, it calculates the new cost and updates the distance and previous node if a shorter path is found.
- Finally, it reconstructs the path from the end node to the start node using the `previous` dictionary.

### Example Usage
- In the `if __name__ == "__main__":` block, a graph is created with nodes A to F and their respective neighbors with edge weights.
- The shortest path from node A to node F is calculated using the `shortest_path` method and printed.

### External Libraries
- The code uses the `heapq` module for the priority queue implementation.

### Example Usage:
```python
if __name__ == "__main__":
    graph = Graph()
    graph.add_node("A", [("B", 4), ("C", 2)])
    graph.add_node("B", [("A", 4), ("C", 1), ("D", 5)])
    graph.add_node("C", [("A", 2), ("B", 1), ("D", 8), ("E", 10)])
    graph.add_node("D", [("B", 5), ("C", 8), ("E", 2), ("F", 6)])
    graph.add_node("E", [("C", 10), ("D", 2), ("F", 3)])
    graph.add_node("F", [("D", 6), ("E", 3)])

    print("Shortest path from A to F:", graph.shortest_path("A", "F"))
```

This code snippet demonstrates how to create a graph, define nodes and their connections, and find the shortest path between two nodes using Dijkstra's algorithm.
  
  ## Component Code
  ```jsx
  import heapq

class Graph:
    def __init__(self):
        self.nodes = {}

    def add_node(self, label, neighbors):
        self.nodes[label] = neighbors

    def shortest_path(self, start, end):
        queue = [(0, start)]
        distances = {node: float('inf') for node in self.nodes}
        distances[start] = 0
        previous = {node: None for node in self.nodes}
        visited = set()

        while queue:
            current_cost, current_node = heapq.heappop(queue)

            if current_node in visited:
                continue

            visited.add(current_node)

            for neighbor, cost in self.nodes[current_node]:
                if neighbor in visited:
                    continue

                new_cost = current_cost + cost
                if new_cost < distances[neighbor]:
                    distances[neighbor] = new_cost
                    previous[neighbor] = current_node
                    heapq.heappush(queue, (new_cost, neighbor))

        path = []
        at = end
        while at is not None:
            path.append(at)
            at = previous[at]

        return path[::-1]

if __name__ == "__main__":
    graph = Graph()
    graph.add_node("A", [("B", 4), ("C", 2)])
    graph.add_node("B", [("A", 4), ("C", 1), ("D", 5)])
    graph.add_node("C", [("A", 2), ("B", 1), ("D", 8), ("E", 10)])
    graph.add_node("D", [("B", 5), ("C", 8), ("E", 2), ("F", 6)])
    graph.add_node("E", [("C", 10), ("D", 2), ("F", 3)])
    graph.add_node("F", [("D", 6), ("E", 3)])

    print("Shortest path from A to F:", graph.shortest_path("A", "F"))
  ```
  