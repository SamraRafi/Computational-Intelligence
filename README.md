# Differential Evolution Computational-Intelligence
The project experiments with the use of Differential Evolution in the class of EAs to optimize the Policy of an Q learning Tic Tac Toe Agent, by evolving a set of Q-tables in order to converge to a population that can beat a learnt agent.

Reinforcement Learning:
An agent Opp is trained initially via Reinforcement Learning over 100,000 games of TicTacToe
The agent maintains a Q-table which it updates after the termination of each game via back propagation using the Bellman Equation to update its Q-Values as given below:
Qt+1(st, at)  Qt(st, at) + ( r+  maxaQ(st+1, a) - Qt(st, at) ) 

## Schema
Initialization:
N agents are trained against Opp for 100 episodes during which each agent learns its Q table using Reinforcement Learning. 
These tables are initialized as the first generation.

Fitness Evaluation:
An individual here is a Q-table, which is a representation of a TicTacToe agent's learned strategy. 
The fitness is calculated by having the agent play a series of games against the opponent Opp. 
The agent gets 1 for each win, -1 for each loss, and gets 0.5 for each draw summed over all games in one run 
To reduce variation in the agent’s gameplay results, the total fitness is averaged over 10 runs.

Mutation:
For each base Q-table in the population, two other Q-tables are randomly selected. 
For each state-action pair in the base Q-table, if the same action exists in the selected Q-tables:
The reward for that action is updated by adding the difference of the rewards in the selected Q-tables, scaled by a mutation factor. 
This creates a new population of mutated Q-tables.

Crossover:
For each Q-table in the mutated population, a Q-table is selected using Fitness Proportional Selection (FPS).
For each state in the selected Q-table, if the same state exists in the mutated Q-table, with a probability equal to the crossover rate, the state-action pairs for that state in the mutated Q-table are replaced with the state-action pairs from the selected Q-table. This creates a new population of trial Q-tables.

Fitness Based Tournament Selection:
The algorithm uses a Tournament Survival selection mechanism. The tournament pool comprises the original population and the trial population. 
Two individuals are randomly chosen from the combined population, and the one with the higher fitness is selected.
This process is repeated until a new population of size N is formed. This new population becomes the current population for the next generation.

## Experimentation Results

Using Tournament Selection, the Best population and Average population stabilized over 20 Generations. However, the population did not converge to the most fit individual

![image](https://github.com/user-attachments/assets/65b078bc-f266-436e-9ac9-da76a7b78340)

The second run resulted in an overall decreasing trend in the fitness scores, indicating that the selection schema has a possibility for losing the local optima found by exploiting sub-optimal solutions.
![image](https://github.com/user-attachments/assets/cd5c1b8c-298e-448c-b876-3df6e4e939a0)

## Conclusion and Future Works

The algorithm has a lot of potential for refinement in terms of the population’s stability,  convergence, overall performance as well as time complexity.

- A steady-state approach: Retaining well performing members of the current generation into the next generation to stabilize the overall trend in the generations.
- Changes to the Mutation and Crossover mechanism to explore more game states before stagnating to a local optima.
- Improving the fitness function to better capture the agent’s performance.
- Mixed Evolution/Learning approach to incorporate periodic Reinforcement Learning to improve the learned state space of a population
