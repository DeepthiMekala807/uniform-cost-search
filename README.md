import heapq

def uniform_cost_search(graph, start, goal):
 
    frontier = []
    heapq.heappush(frontier, (0, start, [start]))
    explored = set()
    
    while frontier:
        cumulative_cost, current_node, path = heapq.heappop(frontier)
        
        if current_node == goal:
            return path, cumulative_cost
        
        if current_node not in explored:
            explored.add(current_node)
            
            for neighbor, edge_cost in graph.get(current_node, {}).items():
                if neighbor not in explored:
                    new_cost = cumulative_cost + edge_cost
                    new_path = path + [neighbor]
                    heapq.heappush(frontier, (new_cost, neighbor, new_path))
    
    return None, float('inf')  

graph = {
    'A': {'B': 4, 'C': 5},
    'B': {'D': 9, 'C': 11, 'E': 7},
    'C': {'E': 3},
    'D': {'E': 13, 'F': 2},
    'E': {'F': 6},
}


start = 'A'
goal = 'F'
path, total_cost = uniform_cost_search(graph, start, goal)

if path:
    print(f"Optimal Path: {' -> '.join(path)}")
    print(f"Total Cost: {total_cost}")
else:
    print("No path found!")
