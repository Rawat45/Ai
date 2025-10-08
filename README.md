import random

def simulate_biased_coin_tosses(num_tosses, bias_for_heads):
    """
    Simulates a series of biased coin tosses.

    Args:
        num_tosses (int): The total number of coin tosses to simulate.
        bias_for_heads (float): The probability of getting heads (between 0 and 1).

    Returns:
        tuple: A tuple containing the count of heads and tails.
    """
    heads_count = 0
    tails_count = 0
    for _ in range(num_tosses):
        if random.random() < bias_for_heads:
            heads_count += 1
        else:
            tails_count += 1
    return heads_count, tails_count

# --- Simulation Parameters ---
number_of_tosses = 1000
# Example bias: 0.6 means 60% chance of heads
# Adjust this value to reflect the actual bias of your coin
coin_bias_for_heads = 0.6 

# Perform the simulation
heads, tails = simulate_biased_coin_tosses(number_of_tosses, coin_bias_for_heads)

# Calculate probabilities from the simulation
probability_of_heads_simulated = heads / number_of_tosses
probability_of_tails_simulated = tails / number_of_tosses

print(f"Simulation Results for {number_of_tosses} tosses (Bias for Heads: {coin_bias_for_heads}):")
print(f"Number of Heads: {heads}")
print(f"Number of Tails: {tails}")
print(f"Estimated Probability of Heads: {probability_of_heads_simulated:.4f}")
print(f"Estimated Probability of Tails: {probability_of_tails_simulated:.4f}")





from collections import deque

def bfs_shortest_path(adj, src, dest):
    q = deque([[src]])
    visited = {src}
    while q:
        path = q.popleft()
        node = path[-1]
        if node == dest:
            return path
        for nei in adj[node]:
            if nei not in visited:
                visited.add(nei)
                q.append(path + [nei])
    return []

# Example
adj = {
    0: [1, 2],
    1: [0, 3],
    2: [0, 4],
    3: [1, 5],
    4: [2, 5],
    5: [3, 4]
}

print(bfs_shortest_path(adj, 0, 5))

