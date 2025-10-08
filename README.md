 import random
from collections import deque

# --- Biased Coin Toss ---
def simulate_coin_tosses(n, bias):
    heads = sum(1 for _ in range(n) if random.random() < bias)
    return heads, n - heads

heads, tails = simulate_coin_tosses(1000, 0.6)
print(f"Heads: {heads}, Tails: {tails}")
print(f"P(Heads): {heads/1000:.4f}, P(Tails): {tails/1000:.4f}")


# --- BFS Shortest Path ---
def bfs(adj, start, end):
    q = deque([[start]])
    visited = {start}
    while q:
        path = q.popleft()
        if path[-1] == end:
            return path
        for neighbor in adj[path[-1]]:
            if neighbor not in visited:
                visited.add(neighbor)
                q.append(path + [neighbor])
    return []

graph = {0:[1,2], 1:[0,3], 2:[0,4], 3:[1,5], 4:[2,5], 5:[3,4]}
print("Shortest path from 0 to 5:", bfs(graph, 0, 5))
