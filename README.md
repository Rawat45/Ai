import random

# Bayes calculation
def bayes_alarm(P_fault, P_alarm_given_fault, P_alarm_given_no_fault):
    P_no_fault = 1 - P_fault

    numerator = P_alarm_given_fault * P_fault
    denominator = numerator + P_alarm_given_no_fault * P_no_fault

    return numerator / denominator


# SIMULATION for 10,000 cases
def simulate_alarm_cases(n=10000, P_fault=0.01, P_alarm_given_fault=0.95, P_alarm_given_no_fault=0.02):
    alarm_count = 0
    true_fault_with_alarm = 0

    for _ in range(n):
        # randomly check if a device actually has a fault
        has_fault = random.random() < P_fault

        # based on fault, trigger alarm with respective probability
        if has_fault:
            alarm = random.random() < P_alarm_given_fault
        else:
            alarm = random.random() < P_alarm_given_no_fault

        # Count alarms
        if alarm:
            alarm_count += 1
            if has_fault:
                true_fault_with_alarm += 1

    experimental_prob = true_fault_with_alarm / alarm_count if alarm_count else 0
    return experimental_prob


# GIVEN PROBABILITIES
P_fault = 0.01
P_alarm_given_fault = 0.95
P_alarm_given_no_fault = 0.02

# BAYES RESULT
bayes_result = bayes_alarm(P_fault, P_alarm_given_fault, P_alarm_given_no_fault)
print("Bayes Probability (Fault | Alarm):", bayes_result)

# SIMULATION RESULT
simulated_prob = simulate_alarm_cases()
print("Simulated Probability (Fault | Alarm) for 10,000 cases:", simulated_prob)

BFS Traversal
from collections import deque

def bfs(graph, start):
    visited = set()
    q = deque([start])

    while q:
        node = q.popleft()
        if node not in visited:
            print(node, end=" ")
            visited.add(node)
            for neigh in graph[node]:
                if neigh not in visited:
                    q.append(neigh)

graph = {
    'A':['B','C'],
    'B':['D','E'],
    'C':['F'],
    'D':[],
    'E':['F'],
    'F':[]
}

bfs(graph, 'A')

BFS With Goal Node
from collections import deque

def bfs_goal(graph, start, goal):
    visited = set()
    q = deque([start])

    while q:
        node = q.popleft()
        if node == goal:
            print("Goal found:", node)
            return
        if node not in visited:
            visited.add(node)
            for neigh in graph[node]:
                if neigh not in visited:
                    q.append(neigh)

graph = {
    'A':['B','C'],
    'B':['D','E'],
    'C':['F'],
    'D':[],
    'E':['F'],
    'F':[]
}

bfs_goal(graph, 'A', 'E')

DFS Traversal
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()

    print(start, end=" ")
    visited.add(start)

    for neigh in graph[start]:
        if neigh not in visited:
            dfs(graph, neigh, visited)

graph = {
    'A':['B','C'],
    'B':['D','E'],
    'C':['F'],
    'D':[],
    'E':['F'],
    'F':[]
}

dfs(graph, 'A')

DFS Path From Start to Goal
def dfs_path(graph, start, goal, path=None):
    if path is None:
        path = []

    path.append(start)

    if start == goal:
        return path

    for neigh in graph[start]:
        if neigh not in path:
            result = dfs_path(graph, neigh, goal, path)
            if result:
                return result

    path.pop()
    return None

graph = {
    'A':['B','C'],
    'B':['D','E'],
    'C':['F'],
    'D':[],
    'E':['F'],
    'F':[]
}

print(dfs_path(graph, 'A', 'F'))

Depth Limited Search
def dls(graph, start, goal, limit):
    def helper(node, depth):
        if depth > limit:
            return None
        if node == goal:
            return [node]

        for neigh in graph[node]:
            path = helper(neigh, depth + 1)
            if path:
                return [node] + path
        return None

    return helper(start, 0)

graph = {
    'A':['B','C'],
    'B':['D','E'],
    'C':['F'],
    'D':[],
    'E':['F'],
    'F':[]
}

print(dls(graph, 'A', 'E', 2))

Hill Climbing
def f(x):
    return -(abs(x-5)) + 10

def hill_climbing():
    x = 0          # starting point
    step = 1

    while True:
        left = f(x - step) if x - step >= 0 else -999
        right = f(x + step) if x + step <= 10 else -999
        current = f(x)

        if left > current:
            x = x - step
        elif right > current:
            x = x + step
        else:
            break

    return x, f(x)

print(hill_climbing())

Dice Simulation
import random

def dice_sim(n):
    count = [0]*6

    for _ in range(n):
        r = random.randint(1,6)
        count[r-1] += 1

    for i in range(6):
        print(f"{i+1}: Experimental = {count[i]/n}, Theoretical = {1/6}")

dice_sim(10000)

Coin Toss Simulation
import random

def coin_sim(n, p_head=0.5):
    heads = 0

    for _ in range(n):
        if random.random() < p_head:
            heads += 1

    tails = n - heads
    print("Heads:", heads/n)
    print("Tails:", tails/n)

print("Fair coin:")
coin_sim(10000)

print("\nBiased coin (p=0.7):")
coin_sim(10000, 0.7)

Medical Test Bayes
def bayes_test(P_disease, P_positive_given_disease, P_positive_given_healthy):
    P_healthy = 1 - P_disease

    numerator = P_positive_given_disease * P_disease
    denominator = numerator + P_positive_given_healthy * P_healthy

    return numerator / denominator

print(bayes_test(0.01, 0.9, 0.05))

🔥 PROLOG PROGRAM — Disease Diagnosis
symptom(john, fever).
symptom(john, cough).
symptom(john, fatigue).

disease(flu, fever).
disease(flu, cough).
disease(flu, fatigue).

has_disease(Patient, Disease) :-
    disease(Disease, Symptom),
    symptom(Patient, Symptom).

explain(Patient, Disease) :-
    has_disease(Patient, Disease),
    write(Patient), write(' has symptoms of '), write(Disease).

🔥 PROLOG — Plant Disease Expert System
symptom(plant1, yellow_leaves).
symptom(plant1, wilting).

disease(fungal_infection, yellow_leaves).
disease(fungal_infection, wilting).

affected(Plant, Disease) :-
    disease(Disease, S),
    symptom(Plant, S).

explain(Plant, Disease) :-
    affected(Plant, Disease),
    write('Diagnosed: '), write(Disease), nl,
    write('Because plant shows symptom: '), write(S).
