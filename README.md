# firefighterapplication
This program simulates the spread of an infection on a 6x6 grid graph and the effect of deploying firefighters to protect vertices from being infected. It compares the effectiveness of deploying 3 firefighters versus 4 firefighters over multiple simulation runs.
1. Graph Creation
   ```
   G = nx.grid_2d_graph(6, 6)
   pos = dict((n, n) for n in G.nodes())
   ```
   This initializes a 6x6 grid graph using NetworkX, with `pos` storing the positions of the nodes to facilitate plotting the graph.

2. Drawing Function
   ```
   def draw_graph(G, pos, infected, protected, timestep):

   ```
   This function, `draw_graph`, visualizes the grid graph at a specific timestep, coloring nodes based on their status: infected (red), protected (blue), or neither (green).

3. Simulation Function
   ```
   def simulate_firefighters(num_firefighters, initial_infected):
   ```
   The `simulate_firefighters` function performs the simulation:
   - It starts with an initial infected vertex.
   - At each timestep, the infection spreads to adjacent vertices unless they are already infected or protected.
   - Firefighters protect a number of uninfected vertices equal to `num_firefighters` per timestep.
   - The simulation continues until no new vertices are infected or the maximum timesteps are reached.
   - The function returns the number of timesteps and the number of protected vertices at the end of the simulation.

4. Running Multiple Simulations
   ```
   def run_multiple_simulations(num_simulations):
   ```
   This function, `run_multiple_simulations`, runs the simulation multiple times (default is 100). For each run, it:
   - Randomly selects an initial infected vertex.
   - Simulates the spread with 3 firefighters and then with 4 firefighters.
   - Records the number of protected vertices for both scenarios.

5. Result Analysis
   ```
   num_simulations = 100
   results_3, results_4 = run_multiple_simulations(num_simulations)

   avg_protected_3 = sum(results_3) / num_simulations
   avg_protected_4 = sum(results_4) / num_simulations

   more_protected_4 = sum(p4 > p3 for p3, p4 in zip(results_3, results_4))
   equal_protected = sum(p4 == p3 for p3, p4 in zip(results_3, results_4))
   ```
   This code slice:
   - Runs the simulations and collects the results.
   - Calculates the average number of protected vertices for 3 and 4 firefighters.
   - Counts how often 4 firefighters protected more vertices than 3 firefighters and how often they protected the same number of vertices.

The overall goal of the code is to empirically determine whether deploying more firefighters (4 vs. 3) results in significantly better protection of the vertices in the grid graph from infection spread.
